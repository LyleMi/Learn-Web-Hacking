端口信息
========================================

常见端口及其脆弱点
----------------------------------------
+ FTP 21
    + 默认用户名密码 ``anonymous:anonymous``
    + 暴力破解密码
    + VSFTP某版本后门
+ SSH 22
    + 暴力破解密码
+ Telent 23
    + 暴力破解密码
+ SMTP 25
    + 无认证时可伪造发件人
+ DNS 53 UDP 
    + 测试域传送漏洞
    + SPF / DMARC Check
    + DDoS
        + DNS Query Flood
        + DNS 反弹
+ SMB 137/139/445
    + 未授权访问
    + 弱口令
+ SNMP 161
    + Public 弱口令
+ LDAP 389
    + 匿名访问
    + 注入
+ Rsync 873
    + 任意文件读写
+ RPC 1025
    + NFS匿名访问
+ MSSQL 1433
    + 弱密码
+ Java RMI 1099
    + RCE
+ Oracle 1521
    + 弱密码
+ NFS 2049
    + 权限设置不当
+ ZooKeeper 2181
    + 无身份认证
+ MySQL 3306
    + 弱密码
+ RDP 3389
    + 弱密码
+ Postgres 5432
    + 弱密码
+ CouchDB 5984
    + 未授权访问
+ Redis 6379
    + 无密码或弱密码
+ Elasticsearch 9200
    + 代码执行
+ Memcached 11211
    + 未授权访问
+ MongoDB 27017
    + 无密码或弱密码
+ Hadoop 50070

除了以上列出的可能出现的问题，暴露在公网上的服务若不是最新版，都可能存在已经公开的漏洞

Web服务
----------------------------------------
+ Jenkins
    + 未授权访问
+ Gitlab
    + 对应版本CVE
+ Zabbix
    + 权限设置不当

批量搜索
----------------------------------------
+ Censys
+ Shodan
+ ZoomEye
