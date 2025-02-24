Reinforcement inspection
========================================

Network equipment
----------------------------------------
- Check the system version number in a timely manner
- Sensitive service settings to access IP/MAC whitelist
- Enable permission hierarchical control
- Close unnecessary services
- Open the operation log

- Close ICMP response

operating system
----------------------------------------

Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Useless user/user group check
- Check empty password account
- User Password Policy
- /etc/login.defs
- /etc/pam.d/system-auth
- Sensitive file permission configuration
- /etc/passwd
- /etc/shadow
- ~/.ssh/
-/VAR/LOG/MESSAGES
- /var/log/secure
-/VAR/LOG/MAILLOG
-/was/log/cron
-/VAR/Log/Spoolols
- /var/log/boot.log
- Is the log open?
- Install patches in time
- Power on
- /etc/init.d
- Check the system clock

Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Exception process monitoring
- Exception start item monitoring
- Exception service monitoring
- Configure system logs
- User Account
- Set password validity period
- Set password strength limit
- Set the number of password retry times
- Install EMET
- Enable PowerShell logging
- Limit the download and execution of the following sensitive files
- ade, adp, ani, bas, bat, chm, cmd, com, cpl, crt, hlp, ht, hta, inf, ins, isp, job, js, jse, lnk, mda, mdb, mde, mdz, msc, msi, msp, mst, pcd, pif, reg, scr, sct, shs, url, vb, vbe, vbs, wsc, wsf, wsh, exe, pif
- Restrictions will adjust the suffix of wscript
- bat, js, jse, vbe, vbs, wsf, wsh
- Domain
- Restrict permissions to join computers to domains
- The principle of using a domain account with minimum permissions
- Reduce the number of non-essential high-authority accounts

application
----------------------------------------

FTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Anonymous login is prohibited
- Modify Banner

SSH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether to disable ROOT login
- Whether to disable password connection

MySQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- File write permission settings
- User authorization table management
- Whether the log is enabled
- Is the version latest?

Web Middleware
----------------------------------------

Apache
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Version number hidden
- Is the version latest?
- Disable partial HTTP verbs
- Close Trace
- Prohibited ``server-status``
- Upload file size limit
- Directory permission settings
- Whether to allow routing rewrite
- Whether to allow column directories
- Log configuration
- Configure timeout to prevent DoS
- Non-master user file read and write restrictions
- httpd.conf
- access.log
- error.log

Nginx
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Disable partial HTTP verbs
- Disable directory traversal
- Check the redirection configuration
- Configure timeout to prevent DoS

IIS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Is the version latest?
- Log configuration
- User password configuration
- ASP.NET feature configuration
- Configure timeout to prevent DoS

JBoss
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- jmx console configuration
- web console configuration

Tomcat
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Disable partial HTTP verbs
- Disable directory columns
- Disable manager function
- User password configuration
- User permission configuration
- Configure timeout to prevent DoS

Password management policy
----------------------------------------
- Length is not less than 8 characters
- Does not exist in existing dictionaries
- No knowledge-based authentication method

Reference link
----------------------------------------
- `awesome windows domain hardening <https://github.com/PaulSec/awesome-windows-domain-hardening>`_
- `customize attack surface reduction <https://docs.microsoft.com/zh-cn/windows/security/threat-protection/microsoft-defender-atp/customize-attack-surface-reduction>`_
