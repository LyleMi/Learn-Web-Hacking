Common intranet protocols
========================================

The order of Windows query name resolution is DNS, mDNS, LLMNR, NBNS.

NetBIOS
----------------------------------------
NetBIOS (Network Basic Input/Output System) is a network-based interaction protocol that usually uses UDP 137, UDP 138, TCP 139 and other ports. When Windows installs the TCP/IP protocol, it will be enabled by default, which may cause network resources without permission verification to be accessed.

Based on NetBIOS, there is the NBNS (NetBIOS Name Service) service, which usually listens on UDP port 137. This service provides three functions: parsing the NetBIOS name to IP, querying the status of a NetBIOS node, and registering/releasing a NetBIOS name.

You can use the ``nbtstat`` tool to manage the network using the NetBIOS protocol.

LLMNR
----------------------------------------
Link-Local Multicast Name Resolution (LLMNR) is a protocol based on the DNS packet format. IPv4 and IPv6 hosts can use this protocol to perform name resolution on hosts on the same local link. This protocol was introduced after Windows Vista.
LLMNR listens on UDP port 5355, accessible via the multicast address 224.0.0.252 (or FF02:0:0:0:0:0:1:3).

mDNS
----------------------------------------
mDNS (multicast DNS) was introduced in Windows 10, listening on UDP port 5353, and the corresponding multicast address is 224.0.0.251 (``FF02::FB``). mDNS mainly enables hosts in the local area network to discover and communicate with each other without a traditional DNS server.

WPAD
----------------------------------------
Web Proxy Auto-Discovery (WPAD) is a method for clients to locate a configuration file URL using DHCP and/or DNS discovery methods. After detecting and downloading the configuration file, it can execute the configuration file to determine which proxy should be used for a specific URL.
