RMI
========================================

Introduction
----------------------------------------
RMI (Remote Method Invocation) allows objects on the client Java virtual machine to call methods on objects in the server Java virtual machine just like local objects. Among them, the RMI standard implementation is Java RMI, and there are different implementations such as Weblogic RMI and Spring RMI.

Two more important concepts in RMI are Stub and Skeleton. Stub and Skeleton implement the same set of interfaces. Stub is called by the client side and does not perform real implementation, but communicates with the server side. Skeleton is the server side, listening for connections from Stub and performing real operations based on the data sent by Stub.

Call Steps
----------------------------------------
- Client calls methods on client helper object Stub
- Client auxiliary object Stub package call information (variable, method name) and send it to server auxiliary object Skeleton via the network
- Server-side auxiliary object Skeleton unpacks the information sent by the client-side auxiliary object, finds out the actually called method and the object where the method is located
- Call the real method on the real service object and return the result to the server auxiliary object Skeleton
- Server side auxiliary object packages the results and sends them to client side auxiliary object Stub
- The client helper object unpacks the return value and returns it to the caller
- Customer gets the return value

Sample
----------------------------------------
A code sample is as follows (from "Enterprise JavaBeans"):

Person interface definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code :: java

public interface Person {
public int getAge() throws Throwable;
public String getName() throws Throwable;
}

Implement Person using PersonServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code :: java

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


Implement Person with Person_Stub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code :: java

import java.io.ObjectOutputStream;
import java.io.ObjectInputStream;
Import java.net.socket;
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

Skeleton implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code :: java

import java.io.ObjectOutputStream;
import java.io.ObjectInputStream;
Import java.net.socket;
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
skel.start ();
}
}

Client implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code :: java

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
The T3 protocol is a protocol used to transfer information between a WebLogic server and other types of Java programs. It is the implementation of the RMI specification by Weblogic. Simply put, T3 can be regarded as an interface that exposes JDNI to users.

JRMP
----------------------------------------
Java Remote Method Protocol (JRMP) is a Java technology-specific protocol used to find and reference remote objects. This is a line layer protocol running under Java Remote Method Call (RMI) and above TCP/IP.

JRMP is a Java-specific stream-based protocol suitable for remote calls between Java, requiring both the client and the server to use Java objects.
