emergency response
========================================

response process
----------------------------------------

event occurs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Operation and maintenance monitoring personnel, customer service auditors, etc. find problems and report them to the next level.

event confirmation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Collect event information, analyze network activity-related programs, logs and data, determine the severity of the event, assess the severity of the problem, and whether to report it to the next level, etc.

incident response
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All departments work together to deal with security issues and solve them concretely to avoid residual problems such as unpatched loopholes and uncleared backdoors.

event closed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After handling the incident, you need to close the incident and write a safety emergency response analysis report to complete the entire emergency process.

Event classification
----------------------------------------
- Virus, Trojan, and worm incidents
- Web server intrusion incident
- Third-party service intrusion incident
- System intrusion events
    - Exploiting Windows vulnerabilities to attack the operating system
- Cyber ​​attacks
    - DDoS / ARP spoofing / DNS hijacking, etc.

Analysis direction
----------------------------------------

File analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Change-based analysis
    - date
    - Document additions and changes
    - Recently used files
- Source code analysis
    - Check source code changes
    - Check and kill WebShell and other backdoors
- System log analysis
- Application log analysis
    - Analyze User-Agent, e.g. ``awvs/burpsuite/w3af/nessus/openvas``
    - Keyword matching for each attack, e.g. ``select/alert/eval``
    - Abnormal requests, consecutive 404 or 500
- ``md5sum`` checks the hashes of commonly used command binaries to check whether rootkits are implanted

process analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Processes that meet the following characteristics
    - CPU or memory resource usage is too high for a long time
    - No signature verification information
    - Process without description information
    - The path of the process is illegal
-dump system memory for analysis
- running processes
- Running services
- Parent process and child process
- Full hash of the background executable
- Installed applications
- Running keys or other persistent programs that are running automatically
- Schedule tasks

Identity information analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Local and domain account users
- Abnormal authentication
- Username in non-standard format

Log analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Antivirus detection records

network analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Firewall configuration
- DNS configuration
- Routing configuration
- Listening ports and related services
- Recently established network connections
- RDP/VPN/SSH etc. sessions

Configuration analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- View configurations such as Linux SE
- View environment variables
- View supporting registry information retrieval, SAM files
- Kernel module

Linux emergency response
----------------------------------------

File analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Recently used files
    - ``find / -ctime -2``
    - ``C:\Documents and Settings\Administrator\Recent``
    - ``C:\Documents and Settings\Default User\Recent``
    - ``%UserProfile%\Recent``
- System log analysis
    - /var/log/
- Focus on location analysis
    - ``/var/log/wtmp`` Login, exit, data exchange, shutdown and restart records
    - ``/var/run/utmp`` records information about the currently logged in user
    - The ``/var/log/lastlog`` file records the last login information of the user, which can be viewed with the lastlog command.
    - ``/var/log/secure`` records files that log in to the system and access data, such as pop3/ssh/telnet/ftp, etc. will be recorded.
    - ``/var/log/cron`` Log information related to scheduled tasks
    - ``/var/log/message`` message and error log after system startup
    - ``/var/log/apache2/access.log`` apache access log
    - ``/etc/passwd`` user list
    - ``/etc/init.d/`` startup items
    - ``/etc/cron*`` scheduled tasks
    - ``/tmp`` temporary directory
    - ``~/.ssh``

User analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``/etc/shadow`` Password login related information
- ``uptime`` View user login time
- ``/etc/sudoers`` sudo user list

process analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` to see if suspicious ports are open
- ``w`` command to view users and their processes
- Analyze boot programs/scripts
    - ``/etc/init.d``
    - ``~/.bashrc``
- View planned or scheduled tasks
    - ``crontab -l``
- ``netstat -an`` / ``lsof`` View process port occupancy

Windows Emergency Response
----------------------------------------

File analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Recently used files
    - ``C:\Documents and Settings\Administrator\Recent``
    - ``C:\Documents and Settings\Default User\Recent``
    - ``%UserProfile%\Recent``
- System log analysis
    - Event Viewer ``eventvwr.msc``

User analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Check if there are new users
- Check whether the server has weak passwords
- View the corresponding key values ​​of the administrator
- ``lusrmgr.msc`` View account changes
- ``net user`` lists the current login account
- ``wmic UserAccount get`` lists all accounts in the current system

process analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` to see if suspicious ports are open
- ``tasklist`` Check if there are any suspicious processes
- Analyze the boot program
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
    - ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\policies\Explorer\Run``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``
    - ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
    - ``(ProfilePath)\Start Menu\Programs\Startup`` startup item
    - ``msconfig`` startup tab
    - ``gpedit.msc`` Group Policy Editor
- View planned or scheduled tasks
    - ``C:\Windows\System32\Tasks\``
    - ``C:\Windows\SysWOW64\Tasks\``
    - ``C:\Windows\tasks\``
    - ``schtasks``
    - ``taskschd.msc``
    - ``compmgmt.msc``
- View startup services
    - ``services.msc``

Log analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Event viewing
    - ``eventvwr.msc``

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- View system environment variables

Reference link
----------------------------------------
- `Hacker intrusion emergency analysis and manual troubleshooting <https://xz.aliyun.com/t/1140>`_
- `Introduction to Forensics Web Chapter <http://www.freebuf.com/column/147929.html>`_
- `Windows system security incident emergency response <https://xz.aliyun.com/t/2524>`_
- `Enterprise Security Emergency Response <https://xz.aliyun.com/t/1632>`_
- `Technical Approaches to Uncovering and Remediating Malicious Activity <https://us-cert.cisa.gov/ncas/alerts/aa20-245a>`_
