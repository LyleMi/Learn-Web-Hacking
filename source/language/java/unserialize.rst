Deserialization
========================================

Introduction
----------------------------------------
Serialization is to convert objects into byte streams to facilitate storage in memory, files, and databases; deserialization is the reverse process, restoring byte streams into objects. It is generally used in scenarios such as remote calls, transferring objects to remote servers through the network, storing objects in databases or waiting for reuse locally. The ``writeObject()`` method of the ``ObjectOutputStream`` class in Java can implement serialization, and the ``readObject()`` method of the ``ObjectInputStream`` class is used for deserialization. If you want to implement deserialization of a class, you must implement the ``Serializable`` interface.

A deserialization vulnerability is considered to exist when a remote service accepts untrusted data for deserialization and an exploitable class exists in the current environment.

sequence data structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``0xaced`` Magic Head / STREAM_MAGIC
- ``0x0005`` Version number / STREAM_VERSION / Reference java.io.ObjectStreamConstants
- ``0x73`` object type identifier
- ``0x72`` class descriptor identifier

Serialization process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ When the ObjectOutputStream instance is initialized, write the magic header and version number into bout (BlockDataOutputStream type)
+ Call ObjectOutputStream.writeObject() to start writing object data
    + ObjectStreamClass.lookup() encapsulates the class description to be serialized (returns the ObjectStreamClass type), and obtains the class name, custom serialVersionUID, serializable fields (returns the ObjectStreamField type) and constructor methods, as well as writeObject and readObject methods, etc.
    + writeOrdinaryObject() writes object data
        + Write object type identifier
        + writeClassDesc() enters the branch writeNonProxyDesc() to write class description data
            + Write class descriptor identifier
            + write class name
            + Write SUID (when SUID is empty, it will be calculated and assigned)
            + Calculate and write serialized attribute flags
            + Write field information data
            + Write Block Data end identifier
            + Write parent class description data
        + writeSerialData() writes the serialized data of the object
            + If the class customizes writeObject(), call this method to write the object, otherwise call defaultWriteFields() to write the field data of the object (if it is a non-primitive type, recursively process the sub-object)

Deserialization process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ When the ObjectInputStream instance is initialized, read the magic header and version number for verification
+ Call ObjectInputStream.readObject() to start reading object data
    + Read object type identifier
    + readOrdinaryObject() reads the data object
        + readClassDesc() reads class description data
            + Read the class descriptor identifier and enter the branch readNonProxyDesc()
            + Read class name
            + Read SUID
            + Read and decompose serialization attribute flags
            + Read field information data
            + resolveClass() obtains the Class object of the class to be deserialized based on the class name. If the acquisition fails, ClassNotFoundException is thrown.
            + skipCustomData() loops to read bytes until the Block Data end flag
            + Read parent class description data
            + In initNonProxy(), determine whether the SUID and class name (excluding package name) of the object and the local object are the same. If they are different, an InvalidClassException will be thrown.
        + ObjectStreamClass.newInstance() obtains and calls the parameterless constructor of the non-Serializable parent class closest to the object (if it does not exist, returns null) to create an object instance
        + readSerialData() reads the serialized data of the object
            + If the class customizes readObject(), call this method to read the object, otherwise call defaultReadFields() to read and fill the field data of the object

exploit
----------------------------------------

Common trigger points
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- JDBC deserialization
- JSON deserialization

Dangerous base libraries
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.mchange:c3p0 0.9.5.2``
- ``com.mchange:mchange-commons-java 0.2.11``
- ``commons-beanutils 1.9.2``
- ``commons-collections 3.1``
- ``commons-fileupload 1.3.1``
- ``commons-io 2.4``
- ``commons-logging 1.2``
- ``org.apache.commons:commons-collections 4.0``
- ``org.beanshell:bsh 2.0b5``
- ``org.codehaus.groovy:groovy 2.3.9``
- ``org.slf4j:slf4j-api 1.7.21``
- ``org.springframework:spring-aop 4.1.4.RELEASE``

Echo mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- echo through middleware features
- echo by throwing an exception
- Echo via OOB
- Echo by writing static files

Vulnerability fixes and protection
----------------------------------------

Hook resolveClass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When using ``readObject()`` to deserialize, the ``resolveClass`` method will be called to read the deserialized class name. You can hook this method to verify the deserialized class. A Demo is as follows

.. code:: java

    @Override
    protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
        if (!desc.getName().equals(SerialObject.class.getName())) {
            throw new InvalidClassException(
                    "Unauthorized deserialization attempt",
                    desc.getName());
        }
        return super.resolveClass(desc);
    }

The above Demo only allows serialization of ``SerialObject``. In this way, you can set a whitelist that allows serialization to prevent deserialization vulnerabilities from being exploited. SerialKiller/Jackson/Weblogic, etc. all use this method for defense.

ValidatingObjectInputStream
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The ``ValidatingObjectInputStream`` class in the Apache Commons IO Serialization package provides the ``accept`` method, which can be used to implement deserialization class white/blacklist control. A demo is as follows

.. code:: java

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
Java 9 provides new features that support serialized data filtering. You can inherit the java.io.ObjectInputFilter class and override the checkInput method to implement a custom filter, and use the ObjectInputStream object's setObjectInputFilter to set the filter to implement deserialization white/blacklist control. This mechanism itself is a new feature for Java 9, but then the official suddenly decided to introduce this enhancement mechanism to support JDK 6, 7, and 8 respectively. This mechanism mainly describes the following mechanisms:

- Provide a mechanism to limit deserialization classes, whitelist or blacklist
- Limit the depth and complexity of deserialization
- Provides a mechanism for verifying classes for RMI remote calling objects
- Define a configurable filtering mechanism, for example, you can define filters by configuring properties files
