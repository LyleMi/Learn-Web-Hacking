信息收集 - Linux
========================================

获取内核，操作系统和设备信息
----------------------------------------
- 版本信息
    - ``uname -a`` 所有版本
    - ``uname -r`` 内核版本信息
    - ``uname -n`` 系统主机名字
    - ``uname -m`` Linux内核架构
- 内核信息 ``cat /proc/version``
- CPU信息 ``cat /proc/cpuinfo``
- 发布信息
    - ``cat /etc/*-release``
    - ``cat /etc/issue``
- 主机名 ``hostname``
- 文件系统 ``df -a``

用户和组
----------------------------------------
- 列出系统所有用户 ``cat /etc/passwd``
- 列出系统所有组 ``cat /etc/group``
- 列出所有用户hash（root）``cat /etc/shadow``
- 用户
    - 查询用户的基本信息 ``finger``
    - 当前登录的用户 ``users`` ``who -a``
- 目前登录的用户 ``w``
- 登入过的用户信息 ``last``
- 显示系统中所有用户最近一次登录信息 ``lastlog``

用户和权限信息
----------------------------------------
- 当前用户 ``whoami``
- 当前用户信息 ``id``
- 可以使用sudo提升到root的用户（root） ``cat /etc/sudoers``
- 列出目前用户可执行与无法执行的指令 ``sudo -l``

环境信息
----------------------------------------
- 打印系统环境信息 ``env``
- 打印系统环境信息 ``set``
- 环境变量中的路径信息 ``echo  $PATH``
- 打印历史命令 ``history``
- 显示当前路径 ``pwd``
- 显示默认系统遍历 ``cat /etc/profile``
- 显示可用的shell ``cat /etc/shells``

服务信息
----------------------------------------
- 查看进程信息 ``ps aux``
- 由inetd管理的服务列表 ``cat /etc/inetd.conf``
- 由xinetd管理的服务列表 ``cat /etc/xinetd.conf``
- nfs服务器的配置 ``cat /etc/exports``

作业和任务
----------------------------------------
- 显示指定用户的计划作业（root） ``crontab -l -u %user%``
- 计划任务 ``ls -la /etc/cron*``

网络、路由和通信
----------------------------------------
- 列出网络接口信息 ``/sbin/ifconfig -a``
- 列出网络接口信息 ``cat /etc/network/interfaces``
- 查看系统arp表 ``arp -a``
- 打印路由信息 ``route``
- 查看dns配置信息 ``cat /etc/resolv.conf``
- 打印本地端口开放信息 ``netstat -an``
- 列出iptable的配置规则 ``iptables -L``
- 查看端口服务映射 ``cat /etc/services``

文件
----------------------------------------
- 最近五天的文件 ``find / -ctime +1 -ctime -5``
- 文件系统细节 ``debugfs``
