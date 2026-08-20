RMI
========================================

Introduction
----------------------------------------
RMI (Remote Method Invocation, remote method invocation) allows objects on the client Java virtual machine to call methods on objects in the server Java virtual machine just like calling local objects. The standard implementation of RMI is Java RMI, in addition to different implementations such as Weblogic RMI and Spring RMI.

The two more important concepts in RMI are Stub and Skeleton. Stub and Skeleton implement the same set of interfaces. Stub is called by the Client and does not implement the actual implementation, but communicates with the Server. Skeleton is the server side, which monitors the connection from the Stub and performs real operations based on the data sent by the Stub.

Calling steps
----------------------------------------
- The client calls the method on the client auxiliary object Stub
- The client auxiliary object Stub packages the calling information (variables, method names) and sends it to the server auxiliary object Skeleton through the network
- The server-side auxiliary object Skeleton unpacks the information sent by the client-side auxiliary object and finds out the method that is actually called and the object where the method is located.
- Call the real method on the real service object and return the result to the server auxiliary object Skeleton
- The server auxiliary object packages the results and sends them to the client auxiliary object Stub.
- The client auxiliary object unpacks the return value and returns it to the caller
- The client gets the return value

Sample
----------------------------------------
A code sample is as follows (from "Enterprise JavaBeans"):

Person interface definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: java

    public interface Person {
        public int getAge() throws Throwable;
        public String getName() throws Throwable;
    }

Implementing Person using PersonServer
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


Implementing Person using Person_Stub
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

Implementation of Skeleton
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

Client implementation
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

T3 protocol
----------------------------------------
The T3 protocol is a protocol used to transmit information between WebLogic servers and other types of Java programs. It is Weblogic's implementation of the RMI specification. Simply put, T3 can be regarded as an interface that exposes JDNI to users.

JRMP
----------------------------------------
Java Remote Method Protocol (JRMP) is a Java technology-specific protocol for finding and referencing remote objects. This is a wire-layer protocol that runs under Java Remote Method Invocation (RMI) and on top of TCP/IP.

JRMP is a Java-specific stream-based protocol suitable for remote calls between Java, requiring the use of Java objects on both the client and the server.
