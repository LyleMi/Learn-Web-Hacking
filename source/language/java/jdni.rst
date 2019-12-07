JNDI
========================================

简介
----------------------------------------
JNDI（Java Naming and Directory Interface，Java命名和目录接口）是为Java应用程序提供命名和目录访问服务的API，允许客户端通过名称发现和查找数据、对象，用于提供基于配置的动态调用。这些对象可以存储在不同的命名或目录服务中，例如RMI、CORBA、LDAP、DNS等。

其中Naming Service类似于哈希表的K/V对，通过名称去获取对应的服务。Directory Service是一种特殊的Naming Service，用类似目录的方式来存取服务。

|jndiarch|

JNDI注入
----------------------------------------
JNDI注入是2016年由pentester在BlackHat USA上的 ``A Journey From JNDI LDAP Manipulation To RCE`` 议题提出的。

其攻击过程如下

1. 攻击者将Payload绑定到攻击者的命名/目录服务中
2. 攻击者将绝对URL注入易受攻击的JNDI查找方法
3. 应用程序执行查找
4. 应用程序连接到攻击者控制的JNDI服务并返回Payload
5. 应用程序解码响应并触发有效负载

攻击载荷
----------------------------------------
JDNI主要有几种攻击载荷：

- CORBA
- IOR
- JNDI Reference
- JNDI Reference
- LDAP
- Remote Location
- Remote Object
- RMI
- Serialized Object

.. |jndiarch| image:: ../../images/jndiarch.gif
