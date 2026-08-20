Reinforcement check
========================================

Network equipment
----------------------------------------
- Check the system version number in time
- Set access IP/MAC whitelist for sensitive services
- Turn on permission hierarchical control
- Turn off unnecessary services
- Open operation log
- Configure abnormal alarms
- Turn off ICMP responses

operating system
----------------------------------------

Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Unused user/group check
- Empty password account check
- User password policy
    - /etc/login.defs
    - /etc/pam.d/system-auth
- Sensitive file permission configuration
    - /etc/passwd
    - /etc/shadow
    - ~/.ssh/
    - /var/log/messages
    - /var/log/secure
    - /var/log/maillog
    - /var/log/cron
    - /var/log/spooler
    - /var/log/boot.log
- Whether the log is turned on
- Install patches promptly
- Start automatically at boot
    - /etc/init.d
- Check system clock

Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Abnormal process monitoring
- Abnormal startup item monitoring
- Abnormal service monitoring
- Configure system logs
- User account
    - Set password validity period
    - Set password strength limits
    -Set the number of password retries
- Install EMET
- Enable PowerShell logging
- Restrict the download and execution of the following sensitive files
    - ade, adp, ani, bas, bat, chm, cmd, com, cpl, crt, hlp, ht, hta, inf, ins, isp, job, js, jse, lnk, mda, mdb, mde, mdz, msc, msi, msp, mst, pcd, pif, reg, scr, sct, shs, url, vb, vbe, vbs, wsc, wsf, wsh, exe, pif
- The restriction will call up the suffix of wscript
    - bat, js, jse, vbe, vbs, wsf, wsh
- domain
    - Restrict permissions to join computers to a domain
    - Domain accounts use the principle of least privilege
    - Reduce the number of unnecessary high-privilege accounts

application
----------------------------------------

FTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Disable anonymous login
- Modify Banner

SSH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether to disable ROOT login
- Whether to disable password connections

MySQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- File write permission settings
- User authorization table management
- Whether logging is enabled
- Is the version latest?

Web middleware
----------------------------------------

Apache
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Version number hidden
- Is the version latest?
- Disable some HTTP verbs
- Turn off Trace
- Disable ``server-status``
- Upload file size limit
- Directory permission settings
- Whether to allow route rewriting
- Whether to allow listing of directories
- Log configuration
- Configure timeout to prevent DoS
- Non-owner user file read and write restrictions
    - httpd.conf
    - access.log
    - error.log

Nginx
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Disable some HTTP verbs
- Disable directory traversal
- Check redirect configuration
- Configure timeout to prevent DoS

IIS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Is the version latest?
- Log configuration
- User password configuration
- ASP.NET function configuration
- Configure timeout to prevent DoS

JBoss
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- jmx console configuration
- web console configuration

Tomcat
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Disable some HTTP verbs
- Disable listing of directories
- Disable manager function
- User password configuration
- User permission configuration
- Configure timeout to prevent DoS

Password management strategy
----------------------------------------
- Length no less than 8 characters
- Does not exist in existing dictionary
- Does not use knowledge-based authentication

Reference link
----------------------------------------
- `awesome windows domain hardening <https://github.com/PaulSec/awesome-windows-domain-hardening>`_
- `customize attack surface reduction <https://docs.microsoft.com/zh-cn/windows/security/threat-protection/microsoft-defender-atp/customize-attack-surface-reduction>`_
