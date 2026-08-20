Basic concepts
========================================

JVM
----------------------------------------
JVM is the core of the Java platform, implemented in machine code, and provides all basic functions required for program execution, such as bytecode parsers, JIT compilers, garbage collectors, etc. Since it is implemented in machine code, it is subject to the same attacks as binary files.

JCL is a standard library that comes with the JVM and contains hundreds of system classes. By default, all system classes are trusted and have all privileges.

JDK
----------------------------------------
Java Development Kit (JDK) is a Java platform released by Oracle Corporation. It has Standard Edition (Java SE), Enterprise Edition (Enterprise Edition, Java EE) and other versions.

At the beginning, JDK was released in binary form, and then on November 17, 2006, Sun released the source code of Java under the GPL license, and then OpenJDK appeared.

JMX
----------------------------------------
JMX (Java Management Extensions, Java Management Extensions) is a framework that embeds management functions into applications. It mainly provides corresponding tools for managing and monitoring applications, system objects, devices, and service-oriented networks. JMX can remotely read values ​​in the system and call methods in the system. When JMX is not configured for authentication or the JDK version is too low and a deserialization vulnerability exists, remote code execution may occur.

JNI
----------------------------------------
JNI (Java Native Interface) is an interface provided by Java to interact with other languages.

JNA
----------------------------------------
JNA (Java Native Access) is a framework on JNI that is used to automatically map Java interfaces to native functions without writing additional JNI code.

OGNL
----------------------------------------
OGNL (Object-Graph Navigation Language) is a powerful expression language. Through simple and consistent expression syntax, it provides functions such as accessing any properties of objects, calling methods of objects, traversing the structure diagram of the entire object, and realizing field type conversion.

OGNL is used in Struts2 and provides a ValueStack class. ValueStack is divided into two parts: root and context. The root is the current action object, and the context is all the content in the ActionContext.

IO model
----------------------------------------
Java encapsulates various IO models of the operating system and forms different APIs.

BIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
BIO (Blocking I/O) is a synchronous blocking I/O mode. The reading and writing of data must be blocked in a thread waiting for its completion.

NIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NIO (New I/O) is a synchronous non-blocking I/O model introduced in Java 1.4. It corresponds to the java.nio package and provides abstractions such as Channel, Selector, and Buffer.

AIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AIO (Asynchronous I/O) was introduced in Java 7 and is an improved version of NIO. It is an asynchronous non-blocking IO model, implemented based on events and callback mechanisms.

reflection
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Java reflection mechanism means that in the running state, for any class, all properties and methods of the class can be known; for any object, any of its methods and properties can be called; this function of dynamically obtaining information and dynamically calling object methods is called the reflection mechanism of the language.

Related classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
================          ===================
Class name Purpose
================          ===================
Entity of class Class
Member variables of Field class
Method class
Constructor method of Constructor class
================          ===================

Class related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- asSubclass(Class<U> clazz)
    - Convert the object of the passed class into an object representing its subclass
- Cast
    - Convert the object into an object representing a class or interface
- getClassLoader()
    - Get the class loader
- getClasses()
    - Returns an array containing objects of all public classes and interface classes in this class
- getDeclaredClasses()
    - Returns an array containing objects of all classes and interface classes in this class
- forName(String className)
    - Return the object of the class based on the class name
- getName()
    - Get the full path name of the class
- newInstance()
    -Create an instance of a class
- getPackage()
    - Get the package of the class
- getSimpleName()
    - Get the name of the class
- getSuperclass()
    - Get the name of the parent class that the current class inherits from
- getInterfaces()
    - Get the class or interface implemented by the current class
- getField(String name)
    - Obtain a public attribute object
- getFields()
    - Get all public property objects
- getDeclaredField(String name)
    - Get an attribute object
- getDeclaredFields()
    - Get all attribute objects
- getAnnotation(Class<A> annotationClass)
    - Returns the public annotation object in this class that matches the parameter type
- getAnnotations()
    - Returns all public annotation objects of this class
- getDeclaredAnnotation(Class<A> annotationClass)
    - Returns all annotation objects in this class that match the parameter type
- getDeclaredAnnotations()
    - Returns all annotation objects of this class
- getConstructor(Class...<?> parameterTypes)
    - Obtain the public constructor in the class that matches the parameter type
- getConstructors()
    - Get all public constructors of this class
- getDeclaredConstructor(Class...<?> parameterTypes)
    - Get the constructor in this class that matches the parameter type
- getDeclaredConstructors()
    - Get all the constructors of this class
- getMethod(String name, Class...<?> parameterTypes)
    - Obtain a public method of this class
- getMethods()
    - Get all public methods of this class
- getDeclaredMethod(String name, Class...<?> parameterTypes)
    - Get a method of this class
- getDeclaredMethods()
    - Get all methods of this class
- isAnnotation()
    - Returns true if it is an annotation type
- isAnnotationPresent(Class<? extends Annotation> annotationClass)
    - Returns true if it is the specified type annotation type
- isAnonymousClass()
    - Returns true if it is an anonymous class
- isArray()
    - Returns true if it is an array class
- isEnum()
    - Returns true if it is an enumeration class
- isInstance(Object obj)
    - Returns true if obj is an instance of this class
- isInterface()
    - Returns true if it is an interface class
- isLocalClass()
    - Returns true if it is a local class
- isMemberClass()
    - Returns true if it is an inner class

Field related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- equals(Object obj)
    - Returns true if the attribute is equal to obj
- get(Object obj)
    - Get the corresponding attribute value in obj
- set(Object obj, Object value)
    - Set the corresponding attribute value in obj

Method related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- invoke(Object obj, Object... args)
    - Pass the object object and parameters to call the method corresponding to the object

Constructor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- newInstance(Object... initargs)
    - Create an object of the class based on the passed parameters
