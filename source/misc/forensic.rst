溯源与入侵应急
========================================

常见检查
----------------------------------------

文件分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 基于变化的分析
    - 日期
    - 文件增改
    - 最近使用文件 
        - ``find / -ctime -2``
        - ``C:\Documents and Settings\Administrator\Recent``
        - ``C:\Documents and Settings\Default User\Recent``
        - ``%UserProfile%\Recent``
- 源码分析
    - 检查源码改动
    - 查杀WebShell等后门
- 系统日志分析
    - Windows: 事件查看器（ ``eventvwr.msc`` ）
    - Linux: /var/log/
- 应用日志分析
    - 分析User-Agent，e.g. ``awvs / burpsuite / w3af / nessus / openvas``
    - 对每种攻击进行关键字匹配，e.g. ``select/alert/eval``
    - 异常请求，连续的404或者500
- ``md5sum`` 检查常用命令二进制文件的哈希，检查是否被植入rootkit
- 重点分析位置
    - ``/var/log/wtmp`` 登录进入，退出，数据交换、关机和重启纪录
    - ``/var/run/utmp`` 有关当前登录用户的信息记录
    - ``/var/log/lastlog`` 文件记录用户最后登录的信息，可用 lastlog 命令来查看。
    - ``/var/log/secure`` 记录登入系统存取数据的文件，例如 pop3/ssh/telnet/ftp 等都会被记录。
    - ``/var/log/cron`` 与定时任务相关的日志信息
    - ``/var/log/message`` 系统启动后的信息和错误日志
    - ``/var/log/apache2/access.log`` apache access log
    - ``/etc/passwd`` 用户列表
    - ``/etc/init.d/`` 开机启动项
    - ``/etc/cron*`` 定时任务
    - ``/tmp`` 临时目录
    - ``~/.ssh``

用户分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Linux
    - ``/etc/shadow`` 密码登陆相关信息
    - ``uptime`` 查看用户登陆时间
    - ``/etc/sudoers`` sudo用户列表
- Windows
    - 查看管理员对应键值
    - ``lusrmgr.msc`` 查看账户变化

进程分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``w`` 命令，查看用户及其进程
- 分析开机自启程序
    - ``/etc/init.d``
    - ``~/.bashrc``
    - ``HKEY_CURRENT_USER\software\micorsoft\windows\currentversion\run``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce``
- 查看计划或定时任务
- ``netstat –an`` / ``lsof`` 查看进程端口占用

配置分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 查看防火墙/DNS/IP等配置
- 查看Linux SE等配置
- 查看环境变量
- 查看配套的注册表信息检索，SAM文件

溯源关联分析方法
----------------------------------------

文档类
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- hash
- ssdeep
- 版本信息（公司/作者/最后修改作者/创建时间/最后修改时间）

可执行文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 特殊端口
- 特殊字符串/密钥
- PDB文件路径

清除日志方式
----------------------------------------
- ``kill <bash process ID>`` 不会存储
- ``set +o history`` 不写入历史记录
- ``unset HISTFILE`` 清除历史记录的环境变量

参考链接
----------------------------------------
- `Web日志安全分析系统实践 <https://xz.aliyun.com/t/2136>`_
- `Web日志安全分析浅谈 <https://xz.aliyun.com/t/1121>`_
- `大型互联网企业入侵检测实战总结 <https://xz.aliyun.com/t/1626/>`_
- `黑客入侵应急分析手工排查 <https://xz.aliyun.com/t/1140>`_
- `同程入侵检测系统 <https://mp.weixin.qq.com/s/kzeAEvz-ejLD71fgb5t8tA>`_
- `取证入门 web篇 <http://www.freebuf.com/column/147929.html>`_
