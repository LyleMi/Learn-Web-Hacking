JDK
========================================

JDK 8
----------------------------------------
- ``sun.net.www.protocol`` no longer supports the gopher protocol

8u251
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The com.sun.org.apache.bcel.internal.util.ClassLoader class was deleted

8u191
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote reference code is not trusted by default, which affects the attack methods of LDAP remote reference code.

8u121
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- RMI has added a deserialization whitelist mechanism
- RMI remote reference code is not trusted by default, which affects RMI remote reference code attack methods

8u113
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` defaults to false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` defaults to false

JDK 7
----------------------------------------

7u201
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote reference code is not trusted by default, which affects the attack methods of LDAP remote reference code.

7u122
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` defaults to false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` defaults to false

7u40
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The ``isInvalid`` method has been added to the ``java.io.File`` class to detect whether the file name contains null bytes.

JDK 6
----------------------------------------

6u211
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP remote reference code is not trusted by default, which affects the attack methods of LDAP remote reference code.

6u141
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` defaults to false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` defaults to false

6u45
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- java.rmi.server.useCodebaseOnly defaults to true, disables automatic loading of remote class files
