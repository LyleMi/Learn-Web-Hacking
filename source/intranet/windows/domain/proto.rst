内网常用协议
========================================

Windows查询名称解析的顺序为DNS、mDNS、LLMNR、NBNS。

NetBIOS
----------------------------------------
NetBIOS（Network Basic Input/Output System）是基于网络的交互协议，通常使用UDP 137、UDP 138、TCP 139等端口。Windows在安装TCP/IP协议时会默认启用该协议，可能导致未设置权限校验的网络资源被访问。

基于NetBIOS有NBNS (NetBIOS Name Service)服务，通常监听在UDP 137端口，该服务提供三种功能：将NetBIOS名称解析到IP、查询某一个NetBIOS节点的状态，注册/释放一个NetBIOS名。

可以使用 ``nbtstat`` 工具利用NetBIOS协议管理网络。

LLMNR
----------------------------------------
链路本地多播名称解析 (Link-Local Multicast Name Resolution, LLMNR)是一个基于DNS数据包格式的协议，IPv4和IPv6的主机可以通过此协议对同一本地链路上的主机执行名称解析。该协议在Windows Vista后被引入。
LLMNR监听UDP 5355端口，可以通过多播地址 224.0.0.252 (或 ``FF02:0:0:0:0:0:1:3``) 访问。

mDNS
----------------------------------------
mDNS (multicast DNS) 在Windows 10中被引入，监听UDP 5353端口，对应的多播地址为 224.0.0.251 ( ``FF02::FB`` ) 。mDNS主要实现了在没有传统DNS服务器的情况下使局域网内的主机实现相互发现和通信。

WPAD
----------------------------------------
网络代理自动发现协议 (Web Proxy Auto-Discovery, WPAD) 是一种客户端使用DHCP和/或DNS发现方法来定位一个配置文件URL的方法。在检测和下载配置文件后，它可以执行配置文件以测定特定URL应使用的代理。
