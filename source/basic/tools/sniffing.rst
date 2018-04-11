嗅探工具
================================

Nmap
--------------------------------

``nmap [<扫描类型>...] [<选项>] {<扫描目标说明>}``

指定目标
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CIDR风格 ``192.168.1.0/24``
- 逗号分割 ``www.baidu.com,www.zhihu.com``
- 分割线 ``10.22-25.43.32``
- 来自文件 ``-iL <inputfile>``
- 排除不需要的host ``--exclude <host1 [, host2] [, host3] ... >`` ``--excludefile <excludefile>``

主机发现
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sL`` List Scan - simply list targets to scan
- ``-sn/-sP`` Ping Scan - disable port scan
- ``-Pn`` Treat all hosts as online -- skip host discovery
- ``-sS/sT/sA/sW/sM`` TCP SYN/Connect()/ACK/Window/Maimon scans
- ``-sU`` UDP Scan
- ``-sN/sF/sX`` TCP Null, FIN, and Xmas scans
- ``-sV`` Probe open ports to determine service/version info
