端口信息
========================================

常见端口及其脆弱点
----------------------------------------
- FTP 21 TCP
    - 默认用户名密码 ``anonymous:anonymous``
    - 暴力破解密码
- SSH 22 TCP
    - 暴力破解密码
- Telent 23 TCP
    - 暴力破解密码
- SMTP 25 TCP
    - 无认证时可伪造发件人
- DNS 53 UDP 
    - 测试域传送漏洞
    - DDoS
        - DNS Query Flood
        - DNS 反弹
- SMB 137/139/445 TCP
- SNMP 161
    - Public 弱口令
- LDAP 389 TCP
    - 匿名访问
- Rsync 873 TCP
    - 任意文件读写
- RPC 1025
    - NFS匿名访问
- MSSQL 1433 TCP
    - 弱密码
- Java RMI 1099
    - RCE
- Oracle 1521 TCP
    - 弱密码
- MySQL 3306 TCP
    - 弱密码
- RDP 3389
    - 弱密码
- postgres 5432
    - 弱密码
- Redis 6379 TCP
    - 无密码或弱密码
- Elasticsearch 9200 TCP
    - 代码执行
- Memcached 11211 TCP
    - 未授权访问
- MongoDB 27017 TCP
    - 无密码或弱密码

除了以上列出的可能出现的问题，暴露在公网上的服务若不是最新版，都可能存在已经公开的漏洞

批量搜索
----------------------------------------
- Censys
- Shodan
- ZoomEye
