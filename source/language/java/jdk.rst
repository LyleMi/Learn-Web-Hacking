JDK
========================================

JDK 6
----------------------------------------

6u45
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- java.rmi.server.useCodebaseOnly 默认为 true，禁用自动加载远程类文件

6u141
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` 默认为false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` 默认为false

6u211
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP远程Reference代码默认不信任，影响LDAP远程Reference代码攻击方式

JDK 7
----------------------------------------

7u40
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``java.io.File`` 类中添加了 ``isInvalid`` 方法，检测文件名中是否包含空字节

7u122
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` 默认为false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` 默认为false

7u201
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP远程Reference代码默认不信任，影响LDAP远程Reference代码攻击方式

JDK 8
----------------------------------------
- ``sun.net.www.protocol`` 不再支持gopher协议

8u113
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``com.sun.jndi.rmi.object.trustURLCodebase`` 默认为false
- ``com.sun.jndi.cosnaming.object.trustURLCodebase`` 默认为false

8u121
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- RMI加入了反序列化白名单机制
- RMI远程Reference代码默认不信任，影响RMI远程Reference代码攻击方式

8u191
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LDAP远程Reference代码默认不信任，影响LDAP远程Reference代码攻击方式
