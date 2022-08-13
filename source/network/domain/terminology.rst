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
