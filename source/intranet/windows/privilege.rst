Permissions
========================================

UAC
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UAC (User Account Control) is a security mechanism introduced in Windows Vista and Windows Server 2008. When some sensitive operations occur, a prompt will pop up to explicitly request system permissions.

When a user logs into Windows, each user will be granted an access token. This token contains security identifier (SID) information, which determines the user's permissions.

Operations that will trigger UAC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Launch the application with administrator rights
- Modify system and UAC settings
- Modify files or directories without permission (%SystemRoot% / %ProgramFiles%, etc.)
- Modify ACL (access control list)
- Install driver
- Add or delete accounts, modify account types, activate guest accounts

ByPass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- DLL related
- Process injection
- Registry

Privilege escalation
----------------------------------------
There are multiple ways to escalate privileges, including exploiting binary vulnerabilities, logic vulnerabilities, and other techniques. The way to gain permissions by exploiting binary vulnerabilities is to exploit the vulnerability running in kernel mode to execute code. For example, UAF or other similar vulnerabilities in the kernel or driver to obtain higher privileges.

Logic vulnerabilities mainly exploit mechanisms with problematic logic in the system. For example, some folders can be written by users but will be started with administrator privileges.

Write arbitrary files using
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In Windows, the sensitive locations that users can write to include the following:

+ User's own files and directories, including ``AppData`` ``Temp``
+ ``C:\`` , user can write by default
+ Subdirectory of ``C:\ProgramData``, by default users can create folders and write files
+ Subdirectory of ``C:\Windows\Temp``, by default users can create folders and write files

Specific ACL information can be viewed with AccessChk, or the ``Get-Acl`` command of PowerShell.

You can use the write permissions on these folders and their subdirectories to write some dlls that may be loaded, and use the loading and execution of the dll to obtain permissions.

MOF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MOF is a file in the Windows system (``c:/windows/system32/wbem/mof/nullevt.mof``) called "Managed Object Format". Its function is to monitor process creation and death every five seconds.

When you have the permission to upload files but do not have a Shell, you can upload a customized mof file to the corresponding location, and the mof will be executed after a certain period of time.

Generally, a vbs script that adds a command to add an administrator user is added to the mof. After execution, a new administrator account will be created.

Credential theft
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Windows native password hash export tool
    - mimikatz
    - lsass
    - wce
    - gsecdump
    - copypwd
    - Pwdump
    - ProcDump
        - https://docs.microsoft.com/en-us/sysinternals/downloads/procdump
- Windows local password cracking tool
    - L0phtCrack
    - SAMInside
    - Ophcrack
- Rainbow table crack
- Native hash + plain text capture
- win8+win2012 plain text capture
- Export of ntds.dit + QuarkPwDump reading analysis
- vssown.vbs + libesedb + NtdsXtract
- ntdsdump
- Use powershell (DSInternals) to analyze hash
- Use ``net use \\%computername% /u:%username%`` to reset password attempts
- When reading is restricted, you can read in the dump file of the blue screen after crashing the operating system.

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Group Policy Preferences vulnerability
- DLL hijacking
- Replace system tools and implement backdoors
- Turn off defender
    - ``Set-MpPreference -disablerealtimeMonitoring $true``
