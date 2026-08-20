Windows
========================================

Local user authentication
----------------------------------------
When Windows performs local login authentication, the operating system will use the password entered by the user as a credential to compare and verify it with the password in the system. User input is received through ``winlogon.exe`` and passed to ``lsass.exe`` for authentication.

``winlogon.exe`` is used to display the login interface after the user logs off, restarts, or locks the screen. ``lsass.exe`` is used to convert the plain text password into the form of NTLM Hash and compare it with the SAM database for authentication.

SAM
----------------------------------------
Security Accounts Manager (SAM) is a mechanism used by the Windows operating system to manage the security of user accounts. The database file used to store Windows operating system passwords. In order to avoid the leakage of plaintext passwords, the SAM file stores plaintext passwords that have been processed by a series of algorithms. The saved Hash is divided into LM Hash and NTLM Hash. When the user performs identity authentication, the entered Hash value will be compared with the Hash value saved in the SAM file.

SAM files are saved in ``%SystemRoot%\system32\config\sam`` and in the registry in ``HKEY_LOCAL_MACHINE\SAM\SAM``, ``HKEY_LOCAL_MACHINE\SECURITY\SAM``. Under normal circumstances, the SAM file is locked and cannot be directly accessed, copied, or moved. Only system user permissions can read and write the file.

Password cracking
----------------------------------------
- Obtain the ``%SystemRoot%\system32\config\sam`` file on the Windows partition by physically touching the host and booting other operating systems
- Get the ``%SystemRoot%\repair\sam._`` file.
- Use tools to export SAM hashes from the registry
- Sniff and analyze SMB messages from the network to obtain password hashes

SPNEGO
----------------------------------------
SPNEGO (SPNEGO: Simple and Protected GSS-API Negotiation) is a security protocol provided by Microsoft that uses the GSS-API authentication mechanism to enable Webservers to share Windows Credentials. It extends Kerberos.
