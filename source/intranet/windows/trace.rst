痕迹清理
========================================

日志
----------------------------------------
- 查看日志 ``eventvwr``
- 伪造日志 ``eventcreate``
- 操作日志
    - 3389登录列表
    - 文件打开日志
    - 文件修改日志
    - 浏览器日志
    - 系统事件
    - 程序安装记录
    - 程序删除记录
    - 程序更新记录
- 登录日志
    - 系统安全日志
- 日志路径
    - 系统日志 ``%SystemRoot%\System32\Winevt\Logs\System.evtx``
    - 安全日志 ``%SystemRoot%\System32\Winevt\Logs\Security.evtx``
    - 应用程序日志 ``%SystemRoot%\System32\Winevt\Logs\Application.evtx``
- 服务日志
    - IIS ``%SystemDrive%\inetpub\logs\LogFiles\W3SVC1\``

注册表
----------------------------------------
- AppCompatFlags
- Background Activity Moderator (BAM)
- MuiCache
- RecentApps
- RunMRU
- ShimCache (AppCompatCache)

注册表键
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- HKEY_LOCAL_MACHINE\system\CurrentControlSet\Services\Eventlog

文件
----------------------------------------

Prefetch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
预读取文件夹，用来存放系统已访问过的文件的预读信息，扩展名为PF。位置在 ``C:\Windows\Prefetch`` 。

JumpLists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
记录用户最近使用的文档和应用程序，方便用户快速跳转到指定文件，位置在 ``%APPDATA%\Microsoft\Windows\Recent`` 。

Amcache / RecentFileCache.bcf
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows中的使用这两个文件来跟踪具有不同可执行文件的应用程序兼容性问题，它可用于确定可执行文件首次运行的时间和最后修改时间。

在Windows 7、Windows Server 2008 R2等系统中，文件保存在 ``C:\Windows\AppCompat\Programs\RecentFileCache.bcf`` ，包含程序的创建时间、上次修改时间、上次访问时间和文件名。

在Windows 8、Windows 10、Windows Server 2012等系统中，文件保存在 ``C:\Windows\AppCompat\Programs\Amcache.hve`` ，包含文件大小、版本、sha1、二进制文件类型等信息。

时间轴
----------------------------------------
Windows时间轴是Windows 10在1803版中引入的一个新特性，会记录访问过的网站、编辑过的文档、运行的程序等，

彻底删除
----------------------------------------
- 多次覆写文件 ``cipher /w:<path>``
- 格式化某磁盘count次 ``format D: /P:<count>``
