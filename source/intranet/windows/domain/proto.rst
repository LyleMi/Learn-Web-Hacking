Common protocols for intranet
========================================

The order of Windows query name resolution is DNS, mDNS, LLMNR, and NBNS.

NetBIOS
----------------------------------------
NetBIOS (Network Basic Input/Output System) is a network-based interactive protocol, which usually uses ports such as UDP 137, UDP 138, TCP 139, etc. Windows will enable this protocol by default when installing TCP/IP protocol, which may cause network resources that do not set permission verification to be accessed.

Based on NetBIOS, it has NBNS (NetBIOS Name Service) service, which usually listens on UDP 137 port. This service provides three functions: parse the NetBIOS name to the IP, query the status of a certain NetBIOS node, and register/release a NetBIOS name.

The network can be managed using the NetBIOS protocol using the ``nbtstat`` tool.

Lamnar
----------------------------------------
Link-Local Multicast Name Resolution (LLMNR) is a protocol based on the DNS packet format. IPv4 and IPv6 hosts can perform name resolution on hosts on the same local link. This protocol was introduced after Windows Vista.
LLMNR listens to UDP port 5355 and can be accessed through the multicast address 224.0.0.252 (or ``FF02:0:0:0:0:0:0:1:3`.).

mDNS
----------------------------------------
mDNS (multicast DNS) was introduced in Windows 10 to listen to UDP 5353 ports, and the corresponding multicast address is 224.0.0.251 ( ``FF02::FB`` ). mDNS mainly implements the hosts in the LAN to realize mutual discovery and communication without traditional DNS servers.

Rain
----------------------------------------
Web Proxy Auto-Discovery (WPAD) is a method in which clients use DHCP and/or DNS discovery methods to locate a configuration file URL. After detecting and downloading the configuration file, it can execute the configuration file to determine which proxy a specific URL should use.
