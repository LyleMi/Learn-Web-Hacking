应急响应
========================================

响应流程
----------------------------------------

事件发生
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
运维监控人员、客服审核人员等发现问题，向上通报。

事件确认
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
收集事件信息、分析网络活动相关程序，日志和数据，判断事件的严重性，评估出问题的严重等级，是否向上进行汇报等。

事件响应
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
各部门通力合作，处理安全问题，具体解决问题，避免存在漏洞未修补、后门未清除等残留问题。

事件关闭
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
处理完事件之后，需要关闭事件，并写出安全应急处理分析报告，完成整个应急过程。

事件分类
----------------------------------------
- 病毒、木马、蠕虫事件
- Web服务器入侵事件
- 第三方服务入侵事件
- 系统入侵事件
    - 利用Windows漏洞攻击操作系统
- 网络攻击事件
    - DDoS / ARP欺骗 / DNS劫持等

分析方向
----------------------------------------

文件分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 基于变化的分析
    - 日期
    - 文件增改
    - 最近使用文件 
- 源码分析
    - 检查源码改动
    - 查杀WebShell等后门
- 系统日志分析
- 应用日志分析
    - 分析User-Agent，e.g. ``awvs / burpsuite / w3af / nessus / openvas``
    - 对每种攻击进行关键字匹配，e.g. ``select/alert/eval``
    - 异常请求，连续的404或者500
- ``md5sum`` 检查常用命令二进制文件的哈希，检查是否被植入rootkit

进程分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 符合以下特征的进程
    - CPU或内存资源占用长时间过高
    - 没有签名验证信息
    - 没有描述信息的进程
    - 进程的路径不合法
- dump系统内存进行分析
- 正在运行的进程
- 正在运行的服务
- 父进程和子进程
- 后台可执行文件的完整哈希
- 已安装的应用程序
- 运行着密钥或其他正在自动运行的持久化程序
- 计划任务

身份信息分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 本地以及域账号用户
- 异常的身份验证
- 非标准格式的用户名

日志分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 杀软检测记录

网络分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 防火墙配置
- DNS配置
- 路由配置
- 监听端口和相关服务
- 最近建立的网络连接
- RDP / VPN / SSH 等会话

配置分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 查看Linux SE等配置
- 查看环境变量
- 查看配套的注册表信息检索，SAM文件
- 内核模块

Linux应急响应
----------------------------------------

文件分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 最近使用文件 
    - ``find / -ctime -2``
    - ``C:\Documents and Settings\Administrator\Recent``
    - ``C:\Documents and Settings\Default User\Recent``
    - ``%UserProfile%\Recent``
- 系统日志分析
    - /var/log/
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
- ``/etc/shadow`` 密码登陆相关信息
- ``uptime`` 查看用户登陆时间
- ``/etc/sudoers`` sudo用户列表

进程分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` 查看是否打开了可疑端口
- ``w`` 命令，查看用户及其进程
- 分析开机自启程序/脚本
    - ``/etc/init.d``
    - ``~/.bashrc``
- 查看计划或定时任务
    - ``crontab -l``
- ``netstat -an`` / ``lsof`` 查看进程端口占用

Windows应急响应
----------------------------------------

文件分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 最近使用文件 
    - ``C:\Documents and Settings\Administrator\Recent``
    - ``C:\Documents and Settings\Default User\Recent``
    - ``%UserProfile%\Recent``
- 系统日志分析
    - 事件查看器 ``eventvwr.msc``

用户分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 查看是否有新增用户
- 查看服务器是否有弱口令
- 查看管理员对应键值
- ``lusrmgr.msc`` 查看账户变化
- ``net user`` 列出当前登录账户
- ``wmic UserAccount get`` 列出当前系统所有账户

进程分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` 查看是否打开了可疑端口
- ``tasklist`` 查看是否有可疑进程
- 分析开机自启程序
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\policies\Explorer\Run``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
    - ``(ProfilePath)\Start Menu\Programs\Startup`` 启动项
    - ``msconfig`` 启动选项卡
    - ``gpedit.msc`` 组策略编辑器
- 查看计划或定时任务
    - ``C:\Windows\System32\Tasks\``
    - ``C:\Windows\SysWOW64\Tasks\``
    - ``C:\Windows\tasks\``
    - ``schtasks``
    - ``taskschd.msc``
    - ``compmgmt.msc``
- 查看启动服务
    - ``services.msc``

日志分析
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 事件查看
    - ``eventvwr.msc``

其他
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 查看系统环境变量

参考链接
----------------------------------------
- `黑客入侵应急分析手工排查 <https://xz.aliyun.com/t/1140>`_
- `取证入门 web篇 <http://www.freebuf.com/column/147929.html>`_
- `Windows 系统安全事件应急响应  <https://xz.aliyun.com/t/2524>`_
- `企业安全应急响应 <https://xz.aliyun.com/t/1632>`_
- `Technical Approaches to Uncovering and Remediating Malicious Activity <https://us-cert.cisa.gov/ncas/alerts/aa20-245a>`_
