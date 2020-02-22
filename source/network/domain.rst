域名系统
========================================

简介
----------------------------------------
DNS是一个简单的请求-响应协议，是将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。DNS使用TCP和UDP协议的53端口。

术语
----------------------------------------

mDNS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Multicast DNS (mDNS)，多播DNS，使用5353端口，组播地址为 ``224.0.0.251`` 或 ``[FF02::FB]`` 。在一个没有常规DNS服务器的小型网络内可以使用mDNS来实现类似DNS的编程接口、包格式和操作语义。mDNS协议的报文与DNS的报文结构相同，但有些字段对于mDNS来说有新的含义。

启动mDNS的主机会在进入局域网后向所有主机组播消息，包含主机名、IP等信息，其他拥有相应服务的主机也会响应含有主机名和IP的信息。

mDNS的域名是用 ``.local`` 和普通域名区分开的。

FQDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FQDN (Fully-Qualified Domain Name) 是域名的完全形态，主要是包含零长度的根标签，例如 ``www.example.com.`` 。

TLD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Top-Level Domain (TLD) 是属于根域的一个域，例如 ``com`` 或 ``jp`` 。

TLD一般可以分为 Country Code Top-Level Domains (ccTLDs) 、Generic Top-Level Domains (gTLDs) 以及其它。

IDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Internationalized Domain Names for Applications (IDNA) 是为了处理非ASCII字符的情况。

CNAME
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CNAME即Canonical name，又称alias，将域名指向另一个域名。

TTL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Time To Live，无符号整数，记录DNS记录过期的时间，最小是0，最大是2147483647 (2^31 - 1)。

请求响应
----------------------------------------

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
DNS解析过程是递归查询的，具体过程如下：

- 用户要访问域名www.example.com时，先查看本机hosts是否有记录或者本机是否有DNS缓存，如果有，直接返回结果，否则向递归服务器查询该域名的IP地址
- 递归缓存为空时，首先向根服务器查询com顶级域的IP地址
- 根服务器告知递归服务器com顶级域名服务器的IP地址
- 递归向com顶级域名服务器查询负责example.com的权威服务器的IP
- com顶级域名服务器返回相应的IP地址
- 递归向example.com的权威服务器查询www.example.com的地址记录
- 权威服务器告知www.example.com的地址记录
- 递归服务器将查询结果返回客户端

根服务器
----------------------------------------
根服务器是DNS的核心，负责互联网顶级域名的解析，用于维护域的权威信息，并将DNS查询引导到相应的域名服务器。

根服务器在域名树中代表最顶级的 ``.`` 域， 一般省略。

13台IPv4根服务器的域名标号为a到m，即a.root-servers.org到m.root-servers.org，所有服务器存储的数据相同，仅包含ICANN批准的TLD域名权威信息。

权威服务器
----------------------------------------
权威服务器上存储域名Zone文件，维护域内域名的权威信息，递归服务器可以从权威服务器获得DNS查询的资源记录。

权威服务器需要在所承载的域名所属的TLD管理局注册，同一个权威服务器可以承载不同TLD域名，同一个域也可以有多个权威服务器。

递归服务器
----------------------------------------
递归服务器负责接收用户的查询请求，进行递归查询并响应用户查询请求。在初始时递归服务器仅有记录了根域名的Hint文件。

DGA
----------------------------------------
DGA（Domain Generate Algorithm，域名生成算法）是一种利用随机字符来生成C&C域名，从而逃避域名黑名单检测的技术手段，常见于botnet中。一般来说，一个DGA域名的存活时间约在1-7天左右。

通信时，客户端和服务端都运行同一套DGA算法，生成相同的备选域名列表，当需要发动攻击的时候，选择其中少量进行注册，便可以建立通信，并且可以对注册的域名应用速变IP技术，快速变换IP，从而域名和IP都可以进行快速变化。

DGA域名有多种生成方式，根据种子类型可以分为确定性和不确定性的生成。不确定性的种子可能会选用当天的一些即时数据，如汇率信息等。

加密方案
----------------------------------------
作为主流的防御方案，DNS加密有五种方案，分别是 DNS-over-TLS (DoT)、DNS-over-DTLS、DNS-over-HTTPS (DoH)、DNS-over-QUIC以及DNSCrypt。

DoT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DoT方案在2016年发表于RFC7858，使用853端口。主要思想是Client和Server通过TCP协议建立TLS会话后再进行DNS传输，Client通过SSL证书验证服务器身份。

DNS-over-DTLS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-DTLS和DoT类似，区别在于使用UDP协议而不是TCP协议。

DoH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DoH方案在发表RFC8484，使用 ``https://dns.example.com/dns-query{?dns}``  来查询服务器的IP，复用https的443端口，流量特征比较小。DoH会对DNS服务器进行加密认证，不提供fallback选项。目前Cloudflare、Google等服务商对DoH提供了支持。

DNS-over-QUIC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-QUIC安全特性和DoT类似，但是性能更高，目前没有合适的软件实现。

DNSCrypt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNSCrypt使用X25519-XSalsa20Poly1305而非标准的TLS，且DNSCrypt的Client需要额外的软件，Server需要的专门的证书。

DNS隧道
----------------------------------------
DNS隧道工具将进入隧道的其他协议流量封装到DNS协议内，在隧道上传输。这些数据包出隧道时进行解封装，还原数据。

参考链接
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 1034 DOMAIN NAMES CONCEPTS AND FACILITIES <https://tools.ietf.org/html/rfc1034>`_
- `RFC 1035 DOMAIN NAMES IMPLEMENTATION AND SPECIFICATION <https://tools.ietf.org/html/rfc1035>`_
- `RFC 1123 Requirements for Internet Hosts -- Application and Support <https://tools.ietf.org/html/rfc1123>`_
- `RFC 3596 DNS Extensions to Support IP Version 6 <https://tools.ietf.org/html/rfc3596>`_
- `RFC 5001 Automated Updates of DNS Security (DNSSEC) Trust Anchors <https://tools.ietf.org/html/rfc5001>`_
- `RFC 5936 DNS Zone Transfer Protocol <https://tools.ietf.org/html/rfc5936>`_
- `RFC 6376 DomainKeys Identified Mail (DKIM) Signatures <https://tools.ietf.org/html/rfc6376>`_
- `RFC 6762 Multicast DNS <https://tools.ietf.org/html/rfc6762>`_
- `RFC 6891 Extension Mechanisms for DNS (EDNS(0)) <https://tools.ietf.org/html/rfc6891>`_
- `RFC 6895 DNS IANA Considerations <https://tools.ietf.org/html/rfc6895>`_
- `RFC 7766 DNS Transport over TCP - Implementation Requirements <https://tools.ietf.org/html/rfc7766>`_
- `RFC 7858 Specification for DNS over Transport Layer Security (TLS) <https://tools.ietf.org/html/rfc7858>`_
- `RFC 8082 NXDOMAIN <https://tools.ietf.org/html/rfc8082>`_
- `RFC 8482 Providing Minimal-Sized Responses to DNS Queries That Have QTYPE=ANY <https://tools.ietf.org/html/rfc8482>`_
- `RFC 8484 DNS Queries over HTTPS (DoH) <https://tools.ietf.org/html/rfc8484>`_
- `RFC 8490 DNS Stateful Operations <https://tools.ietf.org/html/rfc8490>`_
- `RFC 8499 DNS Terminology <https://tools.ietf.org/html/rfc8499>`_

工具
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Unbound <https://github.com/NLnetLabs/unbound>`_
- `bind9 <https://github.com/isc-projects/bind9>`_

研究文章
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `DGA域名的今生前世：缘起、检测、与发展  <https://mp.weixin.qq.com/s/xbf0Qbppk8R0nx89Pb4YTg>`_
- `DNSSEC原理和分析 <https://blog.thecjw.me/?p=1221>`_
- Plohmann D, Yakdan K, Klatt M, et al. A comprehensive measurement study of domain generating malware[C]//25th {USENIX} Security Symposium ({USENIX} Security 16). 2016: 263-278.
- An End-to-End Large-Scale Measurement of DNS-over-Encryption: How Far Have We Come?
