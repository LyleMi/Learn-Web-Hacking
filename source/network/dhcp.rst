DHCP protocol
========================================

Introduction
----------------------------------------
Dynamic Host Configuration Protocol (DHCP) is a network protocol used for local area networks. It is located at the application layer of the OSI model and works using the UDP protocol. It is mainly used to automatically assign IP addresses to users to facilitate unified management by administrators.

The DHCP server uses 67/udp and the client uses 68/udp. DHCP operation is divided into four basic processes, namely requesting IP lease, providing IP lease, selecting IP lease and confirming IP lease. After the client obtains an IP address, it can send an ARP request to avoid IP conflicts caused by overlapping DHCP server address pools.

DCHP message format
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

Reference link
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
