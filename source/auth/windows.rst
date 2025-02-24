Windows
========================================

Local user authentication
----------------------------------------
When Windows is authenticated by local login, the operating system will use the password entered by the user as the credentials to compare and verify with the password in the system. Authentication via ``winlogon.exe`` receive user input to ``lsass.exe``.

``winlogon.exe`` is used to display the login interface after the user logs out, restarts, and locks the screen. ``lsass.exe`` is used to compare authentication with SAM database by turning plaintext passwords into NTLM Hash.

SAM
----------------------------------------
Security Accounts Manager (SAM) is a mechanism used by the Windows operating system to manage the security of user accounts. Database files used to store Windows operating system passwords. In order to avoid plaintext password leakage, the SAM file is stored in the plaintext password. Hash values saved by a series of algorithms are divided into LM Hash and NTLM Hash. When the user authenticates the identity, the input Hash value will be compared with the Hash value saved in the SAM file.

SAM file is saved in ``%SystemRoot%\system3

Password cracking
----------------------------------------
- Get ``%SystemRoot%\system3 on Windows partition by physically touching the host and starting other operating systems
- Get ``%SystemRoot%epair\sam._`` file.
- Export SAM hash values from the registry using tools
- Sniffing and analyzing SMB messages from the network and obtaining password hash from it

Spne
----------------------------------------
SPNEGO (SPNEGO: Simple and Protected GSS-API Negotiation) is a security protocol provided by Microsoft that uses the GSS-API authentication mechanism to enable Webservers to share Windows Credentials, which extends Kerberos.
