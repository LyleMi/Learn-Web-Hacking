Permissions
========================================

UAC
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UAC (User Account Control) is a security mechanism introduced by Windows Vista and Windows Server 2008. When some sensitive operations occur, a prompt will pop up and explicitly require system permissions.

When a user logs into Windows, each user will be granted an access token, which contains information about security identifier (SID) and determines the user's permissions.

Will trigger UAC operation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Start the application with administrator privileges
- Modify system and UAC settings
- Modify files or directories without permissions (%SystemRoot% / %ProgramFiles% etc.)
- Modify ACL (access control list)
- Install the driver
- Add and delete accounts, modify account types, and activate guest accounts

ByPass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- DLL related
- Process Injection
- Registration form

Elevate permissions
----------------------------------------
There are multiple ways to increase permissions, and there are skills to exploit binary vulnerabilities, logical vulnerabilities, etc. The way to obtain permissions using binary vulnerabilities is to use vulnerabilities running in the kernel state to execute code. For example, kernel, UAF in the driver or other similar vulnerabilities to obtain higher permissions.

Logical vulnerabilities mainly exploit some logic problems in the system. For example, some folder users can write to, but will be started with administrator privileges.

Write files at will
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In Windows, the following are the sensitive locations that users can write.

+ User's own files and directories, including ``AppData```````Temp``
+ ``C:\``, by default, users can write to
+ subdirectory of ``C:\ProgramData``, by default, users can create folders and write files
+ subdirectory of ``C:\Windows\Temp``. By default, users can create folders and write files.

Specific ACL information can be viewed by AccessChk or PowerShell's ``Get-Acl`` command.

You can use the write permissions to these folders and their subdirectories to write some dlls that may be loaded, and use the load execution of the dll to obtain permissions.

MOF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MOF is a file (``c:/windows/system32/wbem/mof/nullevt.mof``) in the Windows system, called "Managed Object Format", which is used to monitor process creation and death every five seconds.

When you have permission to upload files but do not have a shell, you can upload the customized mof file to the corresponding location, and this mof will be executed after a certain period of time.

Generally, a vbs script that adds a command to add an administrator user to the mof will be used, and after execution, a new administrator account will be available.

Certificate theft
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Windows Local Password Hash Export Tool
- facial expressions
- lsass
- WCE
- gsecdump
- Copypwd
- Pwdump
- ProcDump
- https://docs.microsoft.com/en-us/sysinternals/downloads/procdump
- Windows local password cracking tool
- L0phtCrack
- SAMInside
- Ophcrack
- Rainbow Table Cracked
- native hash+ plaintext crawling
- win8+win2012 plain text crawling
- Export of ntds.dit + QuarkPwDump read analysis
- vssown.vbs + libesedb + NtdsXtract
- ntdsdump
- Using powershell(DSInternals) to analyze hash
- Number of attempts to reset password using ``net use \%computername% /u:%username%``
- When reading is restricted, you can crash the operating system and read it in the blue screen dump file

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Group Policy Preference Vulnerability
- DLL hijacking
- Replace the system tool to realize the backdoor
- Close the defender
- ``Set-MpPreference -disablerealtimeMonitoring $true``
