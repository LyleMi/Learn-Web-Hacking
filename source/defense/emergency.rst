Emergency response
========================================

Response Process
----------------------------------------

An incident occurred
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the operation and maintenance monitoring personnel, customer service audit personnel find problems, they will inform them to the upper level.

Event confirmation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Collect event information, analyze network activity-related procedures, logs and data, judge the severity of the event, evaluate the severity of the problem, and whether to report it upwards.

Incident Response
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All departments work together to deal with security issues and solve problems in detail to avoid residual problems such as unpatched vulnerabilities and uncleared backdoors.

Event Close
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After handling the incident, it is necessary to close the incident and write a safety emergency response analysis report to complete the entire emergency process.

Event classification
----------------------------------------
- Virus, Trojan, Worm Events
- Web server intrusion event
- Third-party service intrusion incident
- System intrusion incident
- Exploiting the operating system with Windows vulnerabilities
- Cyber Attack Events
- DDoS/ARP spoofing/DNS hijacking, etc.

Analysis direction
----------------------------------------

File Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Change-based analysis
- date
- File addition and modification
- Recent files
- Source code analysis
- Check source code changes
- Check and kill the backdoors such as WebShell
- System log analysis
- Application log analysis
- 分 truck-Agent，e.g. ``awvs / burps ie / w3af / nessus / open-vas``
- Keyword matching for each attack, e.g. ``select/alert/eval``
-Exception request, continuous 404 or 500
- ``md5sum`` Check the hash of common command binary files and check whether they are implanted in rootkit

Process Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Processes that meet the following characteristics
- CPU or memory resource occupies too much for a long time
- No signature verification information
- Processes without description of information
- The path of the process is illegal
- dump system memory for analysis
- Running process
- Running services
- Parent and child processes
- Full hash of background executable
- Installed applications
- Running a key or other persistent program that is running automatically
- Plan tasks

Identity information analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Local and domain account users
- Exceptional authentication
- Usernames in non-standard formats

Log Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Soft-killing detection record

Network Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Firewall configuration
- DNS configuration
- Routing configuration
- Listen to ports and related services
- Recent network connections
- RDP/VPN/SSH and other sessions

Configuration Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Check Linux SE and other configurations
- View environment variables
- View the accompanying registry information retrieval, SAM file
- Kernel Module

Linux Emergency Response
----------------------------------------

File Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Recent files
- ``find / -ctime -2``
- ``C:\Documents and Settings\Administrator\Recent``
- ``C:\Documents and Settings\Default User\Recent``
- ``%UserProfile%\Recent``
- System log analysis
-/was/log/
- Focused analysis location
- ``/var/log/wtmp`` Log in, log out, data exchange, shutdown and restart records
- ``/var/run/utmp`` Information record about the currently logged-in user
- ``/var/log/lastlog`` file records the user's last login information, and can be viewed by the lastlog command.
- ``/var/log/secure`` Files that log in to the system to access data, such as pop3/ssh/telnet/ftp, etc., will be recorded.
- ``/var/log/cron`` Log information related to timing tasks
- ``/var/log/message`` information and error log after system startup
- ``/var/log/apache2/access.log`` apache access log
- ``/etc/passwd`` User list
- ``/etc/init.d/`` Startup item
- ``/etc/cron*`` timed tasks
- ``/tmp`` Temporary Directory
- ``~/.ssh``

User Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``/etc/shadow`` Password login related information
- ``uptime`` View user login time
- ``/etc/sudoers`` sudo user list

Process Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` Check whether the suspicious port is opened
- ``w`` command to view users and their processes
- Analyze the startup program/script
- ``/etc/init.d``
- ``~/.bashrc``
- View scheduled or scheduled tasks
- `` CRONTAB -
- ``netstat -an`` / ``lsof`` View process port occupation

Windows Emergency Response
----------------------------------------

File Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Recent files
- ``C:\Documents and Settings\Administrator\Recent``
- ``C:\Documents and Settings\Default User\Recent``
- ``%UserProfile%\Recent``
- System log analysis
- Event Viewer ``eventvwr.msc``

User Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Check if there are new users
- Check whether the server has weak passwords
- View the administrator's corresponding key values
- ``lusrmgr.msc`` View account changes
- ``net user`` List current logged in account
- ``wmic UserAccount get`` List all accounts in the current system

Process Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``netstat -ano`` Check whether the suspicious port is opened
- ``tasklist`` Check if there are suspicious processes
- Analysis of the startup program
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce``
- `HKEY_LOCAL_MACHINE \ software \ microsoft \ windows \ Currentversion \ runservates`
- `` Hkey_local_machine \ software \ microsoft \ windows \ Currentversion \ Runserics Sit
- ``HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\policies\Explorer\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices``
- ``HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce``
- ``(ProfilePath)\Start Menu\Programs\Startup`` Startup item
- ``msconfig`` Startup Tab
- ``gpedit.msc`` Group Policy Editor
- View scheduled or scheduled tasks
- ``C:\Windows\System32\Tasks\``
- ``C:\Windows\SysWOW64\Tasks\``
- ``C:\Windows	asks\``
- ``schtasks``
- ``taskschd.msc``
- ``compmgmt.msc``
- View Startup Service
- ``services.msc``

Log Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Event View
- ``eventvwr.msc``

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- View system environment variables

Reference link
----------------------------------------
- `Hacking intrusion emergency analysis manual investigation <https://xz.aliyun.com/t/1140>`_
- `Beginner of evidence collection web article <http://www.freebuf.com/column/147929.html>`_
- `Windows System Security Incident Emergency Response <https://xz.aliyun.com/t/2524>`_
- `Enterprise Security Emergency Response <https://xz.aliyun.com/t/1632>`_
- `Technical Approaches to Uncovering and Remediating Malicious Activity <https://us-cert.cisa.gov/ncas/alerts/aa20-245a>`_
