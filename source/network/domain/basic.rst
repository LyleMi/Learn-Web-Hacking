简介
----------------------------------------
DNS是一个简单的请求-响应协议，是将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。DNS使用TCP和UDP协议的53端口。

请求响应
----------------------------------------

DNS记录
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- A
    - 返回域名对应的IPv4地址
- AAAA
- NS
    - 域名服务器
    - 返回该域名由哪台域名服务器解析
- PTR
    - 反向记录
    - 从IP地址到域名的记录
- MX
    - 电子邮件交换记录
    - 记录邮件域名对应的IP地址

响应码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- NOERROR

::

    No error condition

- FORMERR

::

    Format error - The name server was unable to interpret the query

- SERVFAIL

::

    Server failure - The name server was unable to process this query due to a problem with the name server

- NXDOMAIN

::

    this code signifies that the domain name referenced in the query does not exist

- NOTIMP

::

    Not Implemented - The name server does not support the requested kind of query

- REFUSED

::

    Refused - The name server refuses to perform the specified operation for policy reasons

- NODATA

::

    A pseudo RCODE which indicates that the name is valid, for the given class, but [there] are no records of the given type A NODATA response has to be inferred from the answer.


域名系统工作原理
----------------------------------------

解析过程
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS解析过程是递归查询的，具体过程如下：

- 用户要访问域名www.example.com时，先查看本机hosts是否有记录或者本机是否有DNS缓存，如果有，直接返回结果，否则向递归服务器查询该域名的IP地址
- 递归缓存为空时，首先向根服务器查询com顶级域的IP地址
- 根服务器告知递归服务器com顶级域名服务器的IP地址
- 递归向com顶级域名服务器查询负责example.com的权威服务器的IP
- com顶级域名服务器返回相应的IP地址
- 递归向example.com的权威服务器查询www.example.com的地址记录
- 权威服务器告知www.example.com的地址记录
- 递归服务器将查询结果返回客户端

域传送
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS服务器可以分为主服务器、备份服务器和缓存服务器。域传送是指备份服务器从主服务器拷贝数据，并使用得到的数据更新自身数据库。域传送是在主备服务器之间同步数据库的机制。

服务器类型
----------------------------------------

根服务器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
根服务器是DNS的核心，负责互联网顶级域名的解析，用于维护域的权威信息，并将DNS查询引导到相应的域名服务器。

根服务器在域名树中代表最顶级的 ``.`` 域， 一般省略。

13台IPv4根服务器的域名标号为a到m，即a.root-servers.org到m.root-servers.org，所有服务器存储的数据相同，仅包含ICANN批准的TLD域名权威信息。

权威服务器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
权威服务器上存储域名Zone文件，维护域内域名的权威信息，递归服务器可以从权威服务器获得DNS查询的资源记录。

权威服务器需要在所承载的域名所属的TLD管理局注册，同一个权威服务器可以承载不同TLD域名，同一个域也可以有多个权威服务器。

递归服务器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
递归服务器负责接收用户的查询请求，进行递归查询并响应用户查询请求。在初始时递归服务器仅有记录了根域名的Hint文件。
