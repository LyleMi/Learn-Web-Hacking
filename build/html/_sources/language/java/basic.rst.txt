Basic concepts
========================================

JVM
----------------------------------------
JVM is the core of the Java platform and is implemented in machine code, providing all the basic functions required for program execution, such as bytecode parser, JIT compiler, garbage collector, etc. Since it is implemented by machine code, it is also subject to attacks from binary files.

JCL is a standard library that comes with JVM, which contains hundreds of system classes. By default, all system classes are trustworthy and have all privileges.

JDK
----------------------------------------
The Java Development Kit (JDK) is a Java platform released by Oracle, with standard Edition (Java SE), enterprise Edition (Java EE) and other versions.

At the beginning, the JDK was released in binary form, and then on November 17, 2006, Sun released the Java source code under the GPL license, and then OpenJDK appeared.

JMX
----------------------------------------
JMX (Java Management Extensions) is a framework for implanting management functions for applications, mainly providing corresponding tools for managing and monitoring applications, system objects, devices and service-oriented networks. JMX can remotely read values in the system and call methods in the system. Remote code execution may result in deserialization vulnerability when JMX is not configured for authentication or JDK version is too low.

JNI
----------------------------------------
JNI (Java Native Interface) is an interface provided by Java to interact with other languages.

JNA
----------------------------------------
JNA (Java Native Access) is a framework on JNI, which is used to automatically implement the mapping of Java interfaces to native functions without the need to write additional JNI code.

OGNL
----------------------------------------
OGNL (Object-Graph Navigation Language) is a powerful expression language. Through simple and consistent expression syntax, it provides access to any attributes of an object, calling the object method, and traversing the entire object structure diagram. , implement field type conversion and other functions.

OGNL is used in Struts2 and a ValueStack class is provided. ValueStack is divided into two parts: root and context. The current action object in root is the context, and all the contents in the ActionContext are included.

IO model
----------------------------------------
Java encapsulates various IO models of the operating system and forms different APIs.

BIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
BIO (Blocking I/O) is a synchronous blocking I/O mode, and the read and write data must be blocked in a thread and wait for it to complete.

NIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NIO (New I/O) is a synchronous non-blocking I/O model, introduced in Java 1.4, corresponding to the java.nio package, providing abstractions such as Channel, Selector, Buffer, etc.

AIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AIO (Asynchronous I/O) was introduced in Java 7 and is an improved version of NIO. It is an asynchronous non-blocking IO model, implemented based on event and callback mechanisms.

reflection
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Java reflection mechanism refers to the fact that in the running state, all properties and methods of any class can be known; for any object, any methods and properties of it can be called; this dynamic acquisition of information and dynamically calling objects The function of the method is called the reflex mechanism of the language.

Related categories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
================          ===================
Class Name Purpose
================          ===================
Entities of Class
Member variables of Field class
Methods of the Method class
Constructor class constructor
================          ===================

Class Related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- asSubclass(Class<U> clazz)
- Convert the object of the passed class to an object representing its subclass
- Cast
- Convert an object to an object representing a class or an interface
- getClassLoader()
- Get the loader of the class
- getClasses()
- Return an array containing objects of all public classes and interface classes in the class
- getDeclaredClasses()
- Return an array containing objects of all classes and interface classes in the class
- forName(String className)
- Return the object of the class according to the class name
- getName()
- Get the full path name of the class
- newInstance()
- Create an instance of the class
- getPackage()
- Get packages for class
- getSimpleName()
- Get the name of the class
- getSuperclass()
- Get the name of the parent class inherited by the current class
- Getinterfaces ()
- Obtain the class or interface implemented by the current class
- getField(String name)
- Obtain a public property object
- getFields()
- Obtain all public property objects
- getDeclaredField(String name)
- Obtain a certain attribute object
- getDeclaredFields()
- Get all attribute objects
- getAnnotation(Class<A> annotationClass)
- Returns the public annotation object in this class that matches the parameter type
- getAnnotations()
- Return all public annotation objects in this class
- getDeclaredAnnotation(Class<A> annotationClass)
- Returns all annotation objects in this class that match the parameter type
- getDeclaredAnnotations()
- Return all annotation objects in this class
- getConstructor(Class...<?> parameterTypes)
- Obtain the public constructor method in this class that matches the parameter type
- getConstructors()
- Obtain all public constructors of this class
- getDeclaredConstructor(Class...<?> parameterTypes)
- Obtain the constructor method in this class that matches the parameter type
- getDeclaredConstructors()
- Obtain all constructors of this class
- getMethod(String name, Class...<?> parameterTypes)
- Methods to obtain a publicly owned class
- Getmethods ()
- Obtain all public methods of this class
- getDeclaredMethod(String name, Class...<?> parameterTypes)
- Obtain a method of this class
- getDeclaredMethods()
- Get all methods of this class
- isAnnotation()
- Return true if it is an annotation type
- isAnnotationPresent(Class<? extends Annotation> annotationClass)
- Return true if the type annotation type is specified
- isAnonymousClass()
- Return true if it is an anonymous class
- Disagree ()
- Return true if it is an array class
- isEnum()
- Return true if it is an enumeration class
- isInstance(Object obj)
- Return true if obj is an instance of this class
- isInterface()
- Return true if it is an interface class
- isLocalClass()
- Return true if it is a local class
- isMemberClass()
- Return true if it is an inner class

Field-related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- equals(Object obj)
- Return true if the attribute is equal to obj
- get(Object obj)
- Obj's corresponding attribute value
- set(Object obj, Object value)
- Set the corresponding attribute value in obj

Method related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- invoke(Object obj, Object... args)
- Pass the object object and parameters to call the corresponding method of the object

Constructor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- newInstance(Object... initargs)
- Create object of class based on passed parameters
