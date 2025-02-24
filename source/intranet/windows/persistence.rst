Endurance
========================================

Hide files
----------------------------------------
- Create system hidden files
- ``attrib +s +a +r +h filename`` / ``attrib +s +h filename``
- Create hidden files with NTFS ADS (Alternate Data Streams)
- Retain words with Windows
- ``aux|prn|con|nul|com1|com2|com3|com4|com5|com6|com7|com8|com9|lpt1|lpt2|lpt3|lpt4|lpt5|lpt6|lpt7|lpt8|lpt9``

back door
----------------------------------------

sethc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``sethc.exe`` is a sticky key handler called by the Windows system after the user presses shift five times. When there is a write file but no execution permission, you can leave it by replacing ``sethc.exe`` Backdoor, enter shift five times on the password input page to obtain permissions.

Image Hijacking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In higher versions of Windows, replacement programs are system-protected and other techniques are required to implement replacement.

The specific operation is to add the item ``sethc.exe`` under ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Option``, and then add it to the ``sethc.exe`` item ``debugger`` key, the key value is the path to the malicious program.

Timing tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are two types of task planning mechanisms under Windows: ``schtasks`` and ``at``. Among them, ``at` is already deprecated in higher versions of Windows.

Set the command to ``schtasks /create /tn "TEST_OnLogon" /sc onlogon /tr "cmd.exe /c calc.exe"``, ``schtasks /create /tn "TEST_OnStartup" /sc onstart /ru system /tr " cmd.exe /c calc.exe"``` . The delete command is ``schtasks /delete /tn "TEST_OnLogon" /f`` .

Login script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can execute scripts before the user logs in, using the ``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` setting.

You can also set ``UserInitMprLogonScript`` in the ``HKCU\Environment\`` path.

screensaver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can customize screen savers and use the ``HKEY_CURRENT_USER\Control Panel\Desktop`` setting.

Hide users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows can create hidden users by adding ``$`` after the username. This kind of account can be hidden under certain conditions, but it can still be viewed through the control panel.

On the basis of creating hidden users, you can modify the registry to create shadow users. Users created in this way can only be viewed through the registry.

CLR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CLR (Common Language Runtime Compilation) The common language runtime is the running environment built by Microsoft for .NET products, and can be roughly understood as a .NET virtual machine.

The operation of .NET programs cannot be separated from CLR, so the backdoor can be realized by hijacking CLR.

Winlogon Helper DLL backdoor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Winlogon is a Windows component used to handle various activities such as login, logout, loading user profiles during authentication, closing, locking screens, etc. This behavior is managed by the registry, which defines which processes are started during Windows login. Therefore, you can rely on this registry to maintain permissions.

The registry location is as follows:

- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`` for executing exe programs
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit`` for exe program
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify`` for executing dll files

Self-start
----------------------------------------

Registry-based self-start
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
By writing the corresponding key value in the registry, the program can be started automatically, mainly ``Run`` and ``RunOnce``. The difference between RunOnce and Run is that the key value of RunOnce only works once, and after execution, it is completed. It will be deleted automatically.

The registry is as follows:

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnceEx``

The policy-based self-start registry settings are as follows:

- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run``

Set the boot folder registry location as follows:

- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders``
- ``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders``

Set the service startup item registry location as follows:

- `` Hkey_local_machine \ software \ microsoft \ windows \ Currentversion \ Runserics Sit
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- `HKEY_LOCAL_MACHINE \ software \ microsoft \ windows \ Currentversion \ runservates`
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``

User-boot locations ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit``, ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell``, where the ``Userinit`` key allows Specifies multiple programs separated by commas.

If the user starts the screen saver, you can also start the following through the screen saver. The relevant registry key values are:

- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveActive``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaverIsSecure``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\ScreenSaveTimeOut``
- ``HKEY_CURRENT_USER\Control Panel\Desktop\SCRNSAVE.EXE``

Self-start based on specific directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The self-start directory, the ``C:\Users\Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`` directory is effective for specific users, the ``C:\ProgramData\Microsoft\Windows\Start Menu\Programs \StartUp`` is effective for all users. Before NT6, the two directories were ``C:\Documents and Settings\Username\Start Menu\Programs\StartUp`` / ``C:\Documents and Settings\All Users\Start Menu\Programs\StartUp``.
