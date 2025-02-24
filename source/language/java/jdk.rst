JDK
========================================

JDK 8
----------------------------------------
- ``sun.net.www.protocol`` no longer supports the gopher protocol

8U251
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- com.sun.org.apache.bcel.internal.util.ClassLoader class was deleted

8U191
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote Reference code is not trusted by default, affecting the attack method of LDAP remote Reference code

8u121
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- RMI has added deserialization whitelisting mechanism
- RMI remote Reference code is not trusted by default, affecting the attack method of RMI remote Reference code

8u113
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` Default is false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` Default is false

JDK 7
----------------------------------------

7 A 01
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote Reference code is not trusted by default, affecting the attack method of LDAP remote Reference code

7 and 122
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` Default is false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` Default is false

7 and 40
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The ``isInvalid`` method was added to the ``java.io.File`` class to detect whether the file name contains empty bytes

JDK 6
----------------------------------------

6u211
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote Reference code is not trusted by default, affecting the attack method of LDAP remote Reference code

6 rabbits 141
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` Default is false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` Default is false

6u45
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- java.rmi.server.useCodebaseOnly defaults to true, disable automatic loading of remote class files
