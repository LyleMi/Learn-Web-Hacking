DHCP协议
========================================

简介
----------------------------------------
DHCP（Dynamic Host Configuration Protocol，动态主机配置协议）是一个用于局域网的网络协议，位于OSI模型的应用层，使用UDP协议工作，主要用于自动分配IP地址给用户，方便管理员进行统一管理。

DHCP服务器端使用67/udp，客户端使用68/udp。DHCP运行分为四个基本过程，分别为请求IP租约、提供IP租约、选择IP租约和确认IP租约。客户端在获得了一个IP地址以后，就可以发送一个ARP请求来避免由于DHCP服务器地址池重叠而引发的IP冲突。

DCHP 报文格式
----------------------------------------
::

   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     op (1)    |   htype (1)   |   hlen (1)    |   hops (1)    |
   +---------------+---------------+---------------+---------------+
   |                            xid (4)                            |
   +-------------------------------+-------------------------------+
   |           secs (2)            |           flags (2)           |
   +-------------------------------+-------------------------------+
   |                          ciaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          yiaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          siaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          giaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          chaddr  (16)                         |
   +---------------------------------------------------------------+
   |                          sname   (64)                         |
   +---------------------------------------------------------------+
   |                          file    (128)                        |
   +---------------------------------------------------------------+
   |                          options (variable)                   |
   +---------------------------------------------------------------+

参考链接
----------------------------------------
- `DHCP Wiki <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 2131 Dynamic Host Configuration Protocol <https://tools.ietf.org/html/rfc2131>`_
- `RFC 2132 DHCP Options and BOOTP Vendor Extensions <https://tools.ietf.org/html/rfc2132>`_
- `RFC 3046 DHCP Relay Agent Information Option <https://tools.ietf.org/html/rfc3046>`_
- `RFC 3397 Dynamic Host Configuration Protocol (DHCP) Domain Search Option <https://tools.ietf.org/html/rfc3397>`_
- `RFC 3442 Classless Static Route Option for Dynamic Host Configuration Protocol (DHCP) version 4 <https://tools.ietf.org/html/rfc3442>`_
- `RFC 3942 Reclassifying Dynamic Host Configuration Protocol Version Four (DHCPv4) Options <https://tools.ietf.org/html/rfc3942>`_
- `RFC 4242 Information Refresh Time Option for Dynamic Host Configuration Protocol for IPv6 <https://tools.ietf.org/html/rfc4242>`_
- `RFC 4361 Node-specific Client Identifiers for Dynamic Host Configuration Protocol Version Four (DHCPv4) <https://tools.ietf.org/html/rfc4361>`_
- `RFC 4436 Detecting Network Attachment in IPv4 (DNAv4) <https://tools.ietf.org/html/rfc4436>`_
