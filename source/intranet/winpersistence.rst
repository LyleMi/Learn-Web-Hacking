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
- bitsadmin.exe
- cdb.exe
- certutil.exe
    - 可安装、备份、删除、管理和执行证书
    - 证书存储相关功能
- cmd.exe
- cmstp.exe
- csc.exe
- cscript.exe
    - 执行脚本
- expand.exe
    - 展开一个或多个压缩文件
- mofcomp.exe
- msbuild.exe
    - 构建应用程序
- mshta.exe
    - HTML应用
- netsh.exe
- installutil.exe
    - 安装/卸载程序组件
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
- wmic.exe
    - Windows管理工具
- windbg.exe
- wscript.exe
    - 脚本引擎

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

登录脚本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以在用户登录前执行脚本，使用 ``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` 设置。

屏幕保护程序
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以自定义屏幕保护程序，使用 ``HKEY_CURRENT_USER\Control Panel\Desktop`` 设置。

隐藏用户
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows可以使用在用户名后加入 ``$`` 来创建匿名用户，这种方式创建的用户只能通过注册表查看。

CLR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CLR (Common Language Runtime Compilation) 公共语言运行时，是微软为.NET产品构建的运行环境，可以粗略地理解为.NET虚拟机。

.NET程序的运行离不开CLR，因此可以通过劫持CLR的方式实现后门。

UAC
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UAC (User Account Control) 是Windows的一个安全机制，当一些敏感操作发生时，会跳出提示显式要求系统权限。

当用户登陆Windows时，每个用户都会被授予一个access token，这个token中有security identifier (SID) 的信息，决定了用户的权限。

会触发UAC的操作
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 以管理员权限启动应用
- 修改系统、UAC设置
- 修改没有权限的文件或者目录（ %SystemRoot% / %ProgramFiles% 等 ） 
- 修改ACL (access control list)
- 安装驱动
- 增删账户，修改账户类型，激活来宾账户

自启动
----------------------------------------
通过在注册表中写入相应的键值可以实现程序的开机自启动，主要是 ``Run`` 和 ``RunOnce`` ，其中RunOnce和Run区别在于RunOnce的键值只作用一次，执行完毕后会自动删除。

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
