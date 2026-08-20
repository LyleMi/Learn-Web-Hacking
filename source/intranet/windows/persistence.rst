persistence
========================================

Hidden files
----------------------------------------
- Create system hidden files
    - ``attrib +s +a +r +h filename`` / ``attrib +s +h filename``
- Use NTFS ADS (Alternate Data Streams) to create hidden files
- Take advantage of Windows reserved words
    - ``aux|prn|con|nul|com1|com2|com3|com4|com5|com6|com7|com8|com9|lpt1|lpt2|lpt3|lpt4|lpt5|lpt6|lpt7|lpt8|lpt9``

back door
----------------------------------------

sethc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``sethc.exe`` is a sticky key handler called by the Windows system after the user presses shift five times. When there is a file to write but no execution permission, a backdoor can be left by replacing ``sethc.exe``, and the permission can be obtained by entering shift five times on the password input page.

image hijacking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In higher versions of Windows, replacement programs are protected by the system, and other techniques need to be used to achieve replacement.

The specific operation is to add the item ``sethc.exe`` under the ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Option`` in the registry, and then add the ``debugger`` key to the ``sethc.exe`` item. The key value is the path of the malicious program.

scheduled tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are two scheduled task mechanisms under Windows: ``schtasks`` and ``at``. where ``at`` has been deprecated in later versions of Windows.

The setting commands are ``schtasks /create /tn "TEST_OnLogon" /sc onlogon /tr "cmd.exe /c calc.exe"`` , ``schtasks /create /tn "TEST_OnStartup" /sc onstart /ru system /tr "cmd.exe /c calc.exe"`` . The delete command is ``schtasks /delete /tn "TEST_OnLogon" /f`` .

Login script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can execute scripts before the user logs in, using the HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit setting.

This can also be achieved by setting ``UserInitMprLogonScript`` under the ``HKCU\Environment\`` path.

screensaver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can customize the screen saver, using the ``HKEY_CURRENT_USER\Control Panel\Desktop`` setting.

Hide user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can create hidden users by adding ``$`` after the user name. Such accounts can be hidden under certain conditions, but can still be viewed through the Control Panel.

On the basis of creating hidden users, shadow users can be created by modifying the registry. Users created in this way can only be viewed through the registry.

CLR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CLR (Common Language Runtime Compilation) Common Language Runtime is a running environment built by Microsoft for .NET products. It can be roughly understood as a .NET virtual machine.

.NET programs cannot run without the CLR, so backdoors can be implemented by hijacking the CLR.

Winlogon Helper DLL backdoor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Winlogon is a Windows component used to handle various activities such as login, logout, loading user profile during authentication, shutdown, lock screen, etc. This behavior is managed by the registry, which defines which processes are started during Windows login. So you can rely on this registry to maintain permissions.

The registry location is as follows:

- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`` is used to execute exe programs
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` is used to execute exe programs
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify`` is used to execute dll files

self start
----------------------------------------

Registry-based self-starting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
By writing the corresponding key value in the registry, the program can be started automatically at boot, mainly ``Run`` and ``RunOnce``. The difference between RunOnce and Run is that the key value of RunOnce only works once and will be automatically deleted after execution.

The registration form is as follows:

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnceEx``

The policy-based auto-start registry settings are as follows:

- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``

Set the startup folder registry location as follows:

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``

Set the service startup item registry location as follows:

- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``

User self-launch location ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` , ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`` , where the ``Userinit`` key allows specifying multiple programs separated by commas.

If the user starts the screen saver, they can also start it later through the screen saver. The relevant registry key values ​​are:

- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveActive``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaverIsSecure``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveTimeOut``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\SCRNSAVE.EXE``

Auto-start based on specific directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Self-starting directory, ``C:\Users\Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`` directory is effective for a specific user, ``C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`` is effective for all users. Before NT6, the two directories were ``C:\Documents and Settings\Username\Start Menu\Programs\StartUp`` / ``C:\Documents and Settings\All Users\Start Menu\Programs\StartUp`` .
