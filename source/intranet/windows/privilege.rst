权限
========================================

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
