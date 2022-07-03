端口信息
========================================

常见端口及其脆弱点
----------------------------------------
- FTP (21/TCP)
    - 默认用户名密码 ``anonymous:anonymous``
    - 暴力破解密码
    - VSFTP某版本后门
- SSH (22/TCP)
    - 部分版本SSH存在漏洞可枚举用户名
    - 暴力破解密码
- Telent (23/TCP)
    - 暴力破解密码
    - 嗅探抓取明文密码
- SMTP (25/TCP)
    - 无认证时可伪造发件人
- DNS (53/UDP & 53/TCP)
    - 域传送漏洞
    - DNS劫持
    - DNS缓存投毒
    - DNS欺骗
    - SPF / DMARC Check
    - DDoS
        - DNS Query Flood
        - DNS 反弹
    - DNS 隧道
- DHCP 67/68
    - 劫持/欺骗
- TFTP (69/TCP)
- HTTP (80/TCP)
- Kerberos (88/TCP)
    - 主要用于监听KDC的票据请求
    - 用于进行黄金票据和白银票据的伪造
- POP3 (110/TCP & 995/TCP)
    - 爆破
- RPC (135/TCP)
    - wmic 服务利用
- NetBIOS (137/UDP & 138/UDP)
    - 未授权访问
    - 弱口令
- NetBIOS / Samba (139/TCP)
    - 未授权访问
    - 弱口令
- IMAP (143/TCP & 993/TCP)
- SNMP (161/TCP & 161/UDP)
    - Public 弱口令
- LDAP (389/TCP)
    - 用于域上的权限验证服务
    - 匿名访问
    - 注入
- HTTPS (443/TCP)
- SMB (445/TCP)
    - Windows 协议簇，主要功能为文件共享服务
    - ``net use \\192.168.1.1 /user:xxx\username password``
- Linux Rexec (512/TCP & 513/TCP & 514/TCP)
    - 弱口令
- Rsync (873/TCP)
    - 未授权访问
- RPC (1025/TCP)
    - NFS匿名访问
- Java RMI (1090/TCP & 1099/TCP)
    - 反序列化远程命令执行漏洞
- MSSQL (1433/TCP)
    - 弱密码
    - 差异备份 GetShell
    - SA 提权
- Oracle (1521/TCP)
    - 弱密码
- NFS (2049/TCP)
    - 权限设置不当
    - ``showmount <host>``
- ZooKeeper (2171/TCP & 2375/TCP)
    - 无身份认证
- Docker Remote API (2375/TCP)
    - 未限制IP / 未启用TLS身份认证
    - ``http://docker.addr:2375/version``
- MySQL (3306/TCP)
    - 弱密码
    - 日志写WebShell
    - UDF提权
    - MOF提权
- RDP / Terminal Services (3389/TCP)
    - 弱密码
- Postgres (5432/TCP)
    - 弱密码
    - 执行系统命令
- VNC (5900/TCP)
    - 弱密码
- CouchDB (5984/TCP)
    - 未授权访问
- WinRM (5985/TCP)
    - Windows对WS-Management的实现
    - 在Vista上需要手动启动，在Windows Server 2008中服务是默认开启的
- Redis (6379/TCP)
    - 无密码或弱密码
    - 绝对路径写 WebShell
    - 计划任务反弹 Shell
    - 写 SSH 公钥
    - 主从复制 RCE
    - Windows 写启动项
- Kubernetes API Server (6443/TCP && 10250/TCP)
    - ``https://Kubernetes:10250/pods``
- JDWP (8000/TCP)
    - 远程命令执行
- ActiveMQ (8061/TCP)
- Jenkin (8080/TCP)
    - 未授权访问
- Elasticsearch (9200/TCP)
    - 代码执行
    - ``http://es.addr:9200/_plugin/head/``
    - ``http://es.addr:9200/_nodes``
- Memcached (11211/TCP & 11211/UDP)
    - 未授权访问
- RabbitMQ (15672/TCP & 15692/TCP & 25672/TCP)
- MongoDB (27017/TCP)
    - 无密码或弱密码
- Hadoop (50070/TCP & 50075/TCP)
    - 未授权访问

除了以上列出的可能出现的问题，暴露在公网上的服务若不是最新版，都可能存在已经公开的漏洞

常见端口扫描技术
----------------------------------------

全扫描
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
扫描主机尝试使用三次握手与目标主机的某个端口建立正规的连接，若成功建立连接，则端口处于开放状态，反之处于关闭状态。

全扫描实现简单，且以较低的权限就可以进行该操作。但是在流量日志中会有大量明显的记录。

半扫描
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
半扫描也称SYN扫描，在半扫描中，仅发送SYN数据段，如果应答为RST，则端口处于关闭状态，若应答为SYN/ACK，则端口处于监听状态。不过这种方式需要较高的权限，而且现在的大部分防火墙已经开始对这种扫描方式做处理。

FIN扫描
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FIN扫描是向目标发送一个FIN数据包，如果是开放的端口，会返回RST数据包，关闭的端口则不会返回数据包，可以通过这种方式来判断端口是否打开。

这种方式并不在TCP三次握手的状态中，所以不会被记录，相对SYN扫描要更隐蔽一些。

Web服务
----------------------------------------
- Jenkins
    - 未授权访问
- Gitlab
    - 对应版本CVE
- Zabbix
    - 权限设置不当

批量搜索
----------------------------------------
- Censys
- Shodan
- ZoomEye
