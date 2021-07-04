持久化
========================================

隐藏文件
----------------------------------------
- 创建系统隐藏文件
    - ``attrib +s +a +r +h filename`` / ``attrib +s +h filename``
- 利用NTFS ADS (Alternate　Data　Streams) 创建隐藏文件
- 利用Windows保留字
    - ``aux|prn|con|nul|com1|com2|com3|com4|com5|com6|com7|com8|com9|lpt1|lpt2|lpt3|lpt4|lpt5|lpt6|lpt7|lpt8|lpt9``

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
