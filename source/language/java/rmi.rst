RMI
========================================

简介
----------------------------------------
RMI（Remote Method Invocation，远程方法调用）能够让在客户端Java虚拟机上的对象像调用本地对象一样调用服务端Java虚拟机中的对象上的方法。其中RMI标准实现是Java RMI，之外还有Weblogic RMI、Spring RMI等不同的实现。

RMI中比较重要的两个概念是Stub和Skeleton，Stub和Skeleton对同一套接口进行实现，其中Stub由Client端调用，并不进行真正的实现，而是和Server端通信。Skeleton是Server端，监听来自Stub的连接，根据Stub发送的数据进行真正的操作。

调用步骤
----------------------------------------
- 客户调用客户端辅助对象Stub上的方法
- 客户端辅助对象Stub打包调用信息（变量，方法名），通过网络发送给服务端辅助对象Skeleton
- 服务端辅助对象Skeleton将客户端辅助对象发送来的信息解包，找出真正被调用的方法以及该方法所在对象
- 调用真正服务对象上的真正方法，并将结果返回给服务端辅助对象Skeleton
- 服务端辅助对象将结果打包，发送给客户端辅助对象Stub
- 客户端辅助对象将返回值解包，返回给调用者
- 客户获得返回值

样例
----------------------------------------
一份代码样例如下（来自《Enterprise JavaBeans》）：

Person接口定义
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    public interface Person {
        public int getAge() throws Throwable;
        public String getName() throws Throwable;
    }

使用PersonServer实现Person
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    public class PersonServer implements Person {
        private int age;
        private String name;
        public PersonServer(String name, int age) {
            this.age = age;
            this.name = name;
        }
        public int getAge() {
            return age;
        }
        public String getName() {
            return name;
        }
    }


使用Person_Stub实现Person
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    import java.io.ObjectOutputStream;
    import java.io.ObjectInputStream;
    import java.net.Socket;
    public class Person_Stub implements Person {
        private Socket socket;
        public Person_Stub() throws Throwable {
            // connect to skeleton
            socket = new Socket("computer_name", 9000);
        }
        public int getAge() throws Throwable {
            // pass method name to skeleton
            ObjectOutputStream outStream =
                new ObjectOutputStream(socket.getOutputStream());
            outStream.writeObject("age");
            outStream.flush();
            ObjectInputStream inStream =
                new ObjectInputStream(socket.getInputStream());
            return inStream.readInt();
        }
        public String getName() throws Throwable {
            // pass method name to skeleton
            ObjectOutputStream outStream =
                new ObjectOutputStream(socket.getOutputStream());
            outStream.writeObject("name");
            outStream.flush();
            ObjectInputStream inStream =
                new ObjectInputStream(socket.getInputStream());
            return (String)inStream.readObject();
        }
    }

Skeleton的实现
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    import java.io.ObjectOutputStream;
    import java.io.ObjectInputStream;
    import java.net.Socket;
    import java.net.ServerSocket;
    public class Person_Skeleton extends Thread {
        private PersonServer myServer;
        public Person_Skeleton(PersonServer server) {
            // get reference of object server
            this.myServer = server;
        }
        public void run() {
            try {
                // new socket at port 9000
                ServerSocket serverSocket = new ServerSocket(9000);
                // accept stub's request
                Socket socket = serverSocket.accept();
                while (socket != null) {
                    // get stub's request
                    ObjectInputStream inStream =
                        new ObjectInputStream(socket.getInputStream());
                    String method = (String)inStream.readObject();
                    // check method name
                    if (method.equals("age")) {
                        // execute object server's business method
                        int age = myServer.getAge();
                        ObjectOutputStream outStream =
                            new ObjectOutputStream(socket.getOutputStream());
                        // return result to stub
                        outStream.writeInt(age);
                        outStream.flush();
                    }
                    if(method.equals("name")) {
                        // execute object server's business method
                        String name = myServer.getName();
                        ObjectOutputStream outStream =
                            new ObjectOutputStream(socket.getOutputStream());
                        // return result to stub
                        outStream.writeObject(name);
                        outStream.flush();
                    }
                }
            } catch(Throwable t) {
                t.printStackTrace();
                System.exit(0);
            }
        }
        public static void main(String args []) {
            // new object server
            PersonServer person = new PersonServer("Richard", 34);
            Person_Skeleton skel = new Person_Skeleton(person);
            skel.start();
        }
    }

Client实现
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    public class PersonClient {
        public static void main(String [] args) {
            try {
                Person person = new Person_Stub();
                int age = person.getAge();
                String name = person.getName();
                System.out.println(name + " is " + age + " years old");
            } catch(Throwable t) {
                t.printStackTrace();
            }
        }
    }

T3协议
----------------------------------------
T3协议是用于在WebLogic服务器和其他类型的Java程序之间传输信息的协议，是Weblogic对RMI规范的实现。简单来说，可以把T3视为暴露JDNI给用户调用的接口。

JRMP
----------------------------------------
Java远程方法协议（Java Remote Method Protocol，JRMP）是特定于Java技术的、用于查找和引用远程对象的协议。这是运行在Java远程方法调用（RMI）之下、TCP/IP之上的线路层协议。

JRMP是一个Java特有的、适用于Java之间远程调用的基于流的协议，要求客户端和服务器上都使用Java对象。
