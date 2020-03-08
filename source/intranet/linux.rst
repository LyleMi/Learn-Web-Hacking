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
- 内核日志 ``dmesg`` / ``/var/log/dmesg``

用户和组
----------------------------------------
- 列出系统所有用户 ``cat /etc/passwd``
- 列出系统所有组 ``cat /etc/group``
- 列出所有用户hash（root）``cat /etc/shadow``
- 用户
    - 查询用户的基本信息 ``finger``
    - 当前登录的用户 ``users`` ``who -a`` ``/var/log/utmp``
- 目前登录的用户 ``w``
- 登入过的用户信息 ``last`` / ``/var/log/wtmp``
- 显示系统中所有用户最近一次登录信息 ``lastlog`` / ``/var/log/lastlog``
- 登录成功日志 ``/var/log/secure``
- 登录失败日志 ``/var/log/faillog``
- 查看特权用户 ``grep :0 /etc/passwd``
- 查看passwd最后修改时间 ``ls -l /etc/passwd``
- 查看是否存在空口令用户 ``awk -F: 'length($2)==0 {print $1}' /etc/shadow``
- 查看远程登录的账号 ``awk '/\$1|\$6/{print $1}' /etc/shadow``
- 查看具有sudo权限的用户
    - ``cat /etc/sudoers | grep -v "^#\|^$" | grep "ALL=(ALL)"``

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
- 打印历史命令 ``history`` / ``~/.bash_history``
- 显示当前路径 ``pwd``
- 显示默认系统遍历 ``cat /etc/profile``
- 显示可用的shell ``cat /etc/shells``

进程信息
----------------------------------------
- 查看进程信息 ``ps aux``
- 资源占有情况 ``top -c``
- 查看进程关联文件 ``lsof -c $PID``

服务信息
----------------------------------------
- 由inetd管理的服务列表 ``cat /etc/inetd.conf``
- 由xinetd管理的服务列表 ``cat /etc/xinetd.conf``
- nfs服务器的配置 ``cat /etc/exports``
- 邮件信息 ``/var/log/mailog``

计划任务
----------------------------------------
- 显示指定用户的计划作业（root） ``crontab -l -u %user%``
- 计划任务
    - ``/var/spool/cron/*``
    - ``/var/spool/anacron/*``
    - ``/etc/crontab``
    - ``/etc/anacrontab``
    - ``/etc/cron.*``
    - ``/etc/anacrontab``
- 开机启动项
    - ``/etc/rc.d/init.d/``

网络、路由和通信
----------------------------------------
- 列出网络接口信息 ``/sbin/ifconfig -a`` / ``ip addr show``
- 列出网络接口信息 ``cat /etc/network/interfaces``
- 查看系统arp表 ``arp -a``
- 打印路由信息 ``route`` / ``ip ro show``
- 查看dns配置信息 ``cat /etc/resolv.conf``
- 打印本地端口开放信息 ``netstat -an``
- 列出iptable的配置规则 ``iptables -L``
- 查看端口服务映射 ``cat /etc/services``
- Hostname ``hostname -f``
- 查看进程端口情况 ``netstat -anltp | grep $PID``

已安装程序
----------------------------------------
- ``rpm -qa --last`` Redhat
- ``yum list | grep installed`` CentOS
- ``ls -l /etc/yum.repos.d/``
- ``dpkg -l`` Debian
- ``cat /etc/apt/sources.list`` Debian APT
- ``pkg_info`` xBSD
- ``pkginfo`` Solaris
- ``pacman -Q`` Arch Linux

文件
----------------------------------------
- 最近五天的文件 ``find / -ctime +1 -ctime -5``
- 文件系统细节 ``debugfs``
