Deserialization
========================================

Introduction
----------------------------------------
Serialization is to convert objects into byte streams, which are easy to save in memory, files, and databases; deserialization is the reverse process, which restores objects from byte streams. It is generally used in scenarios such as remote calls, transferring objects to remote servers through the network, storing objects to databases or waiting for reuse locally. The ``writeObject()`` method of the ``ObjectOutputStream` class in Java can be serialized, and the ``readObject()`` method of the ``` class ``` class is used for deserialization. If you want to implement deserialization of a class, you will implement the ``Serializable`` interface to it.

When a remote service accepts untrusted data and deserializes it and there are available classes in the current environment, a deserialization vulnerability is considered to exist.

Sequence data structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``0xaced`` Magic Head / STREAM_MAGIC
- ``0x0005`` Version number / STREAM_VERSION / Reference java.io.ObjectStreamConstants
- ``0x73`` object type identification
- ``0x72`` class descriptor identification

Serialization process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+When ObjectOutputStream instance is initialized, write the magic header and version number to bout (BlockDataOutputStream type)
+ Call ObjectOutputStream.writeObject() to start writing object data
+ ObjectStreamClass.lookup() encapsulates the class description to be serialized (returns the ObjectStreamClass type), obtains the class name, custom serialVersionUID, serializable fields (returns the ObjectStreamField type) and constructor methods, as well as writeObject, readObject methods, etc.
+ writeOrdinaryObject() writes object data
+ Write object type identification
+ writeClassDesc() Enter the branch writeNonProxyDesc() Write class description data
+ Write class descriptor identifier
+ Write class name
+ Write to SUID (when SUID is empty, calculation and assignment will be performed)
+ Calculate and write serialized attribute flag bits
+ Write field information data
+ Write Block Data end flag
+ Write parent class description data
+ writeSerialData() writes the serialized data of the object
+ If the class customizes writeObject(), then call this method to write the object. Otherwise, call defaultWriteFields() to write the object field data (if it is a non-primitive type, then process the child object recursively)

Deserialization process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ When ObjectInputStream instance is initialized, read the magic header and version number for verification
+ Call ObjectInputStream.readObject() to start reading object data
+ Read object type identification
+ readOrdinaryObject() reads data object
+ readClassDesc() reads class description data
+ Read the class descriptor identifier and enter the branch readNonProxyDesc()
+ Read the class name
+ Read SUID
+ Read and decompose serialized attribute flag bits
+ Read field information data
+ resolveClass() Get the Class object of the class to be deserialized according to the class name. If the acquisition fails, a ClassNotFoundException will be thrown.
+ skipCustomData() loops to read bytes until the Block Data ends the flag
+ Read parent class description data
+ In initNonProxy(), determine whether the SUID and class name of the object and the local object are the same (excluding the package name). If it is different, an InvalidClassException will be thrown.
+ ObjectStreamClass.newInstance() Gets and calls the parameterless constructor method of the non-Serializable parent class closest to the object (returns null if it does not exist) Create an object instance
+ readSerialData() reads the serialized data of the object
+ If the class customizes readObject(), then call this method to read the object. Otherwise, call defaultReadFields() to read and fill the field data of the object.

Vulnerability exploitation
----------------------------------------

Common trigger points
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- JDBC Deserialization
- JSON Deserialization

A dangerous basic library
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `` com.mchange: C3p0 0.9.5.2``
-`` com
- ``commons-beanutils 1.9.2``
- ``commons-collections 3.1``
- ``commons-fileupload 1.3.1``
- `'Commons-yo 2.4``
- ``commons-logging 1.2``
- ``org.apache.commons:commons-collections 4.0``
- `` Org.Beanshell: BSH 2.0B5``
- ``org.codehaus.groovy:groovy 2.3.9``
- `` org.slf4j: SLF4J-API 1.7.21``
- ``org.springframework:spring-aop 4.1.4.RELEASE``

Echo method
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Echo through middleware features
- Echo by throwing exception
- Echo through OOB
- Echo by writing static files

Vulnerability repair and protection
----------------------------------------

Hook resolveClass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When deserializing using ``readObject()``, the ````` method is called to read the deserialized class name. You can check the deserialized class by hooking this method. A demo is as follows

.. code :: java

@Override
protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
if (!desc.getName().equals(SerialObject.class.getName())) {
throw new InvalidClassException(
"Unauthorized deserialization attempt",
desc.getName());
}
return super.resolveClass(desc);
}

The above demo only allows serialization ``SerialObject``. In this way, a whitelist that allows serialization can be set to prevent deserialization vulnerabilities from being exploited. SerialKiller/Jackson/Weblogic etc. use this method to defend.

ValidatingObjectInputStream
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The ``ValidatingObjectInputStream` class in the Apache Commons IO Serialization package provides the ``accept`` method, which can be used to implement white/blacklist control of the deserialization class. A demo is as follows

.. code :: java

private static Object deserialize(byte[] buffer) throws IOException, ClassNotFoundException , ConfigurationException {
Object obj;
ByteArrayInputStream bais = new ByteArrayInputStream(buffer);
ValidatingObjectInputStream ois = new ValidatingObjectInputStream(bais);
ois.accept(SerialObject.class);
obj = ois.readObject();
return obj;
}

ObjectInputFilter(JEP290)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Java 9 provides new features that support serialized data filtering. You can inherit the ``java.io.ObjectInputFilter`` class override the ``checkInput`` method to implement a custom filter and use the ``ObjectInputStream`` object's ``setObjectInputFilter`` Sets filters to implement deserialization class white/blacklist control. This mechanism itself is a new feature of Java 9, but then the official suddenly decided to introduce the enhancement mechanism downward, supporting JDK 6, 7, 8 respectively. This mechanism mainly describes the following mechanism:

- Provide a mechanism to restrict deserialization classes, whitelists or blacklists
- Limit the depth and complexity of deserialization
- Provides a verification class mechanism for RMI remote call objects
- Define a configurable filtering mechanism, for example, you can define filters by configuring properties files
