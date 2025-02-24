Information collection
========================================

Basic Commands
----------------------------------------
- Hostname ``hostname``
- Query all computer names ``dsquery computer``
- View configuration and patch information
- ``systeminfo``
- ``wmic qfe get description,installedOn /format:csv``
- View version ``ver``
- Process information
- ``tasklist /svc``
- ``wmic process get caption,executablepath,commandline /format:csv``
- ``get-process``
- View all environment variables ``set``
- View scheduled tasks ``schtasks /QUERY /fo LIST /v``
- View installation driver ``DRIVERQUERY``
- View operating system information
- Architecture ``wmic os get osarchitecture``
- System name ``wmic os get caption``
- View the logic disk ``wmic logicaldisk get caption``
- View installed software information ``wmic product get name,version``
- View service information
- ``wmic service list brief``
- ``sc query``
- ``Get-WmiObject win32_service | select PathName``

Domain information
----------------------------------------
- Get the computer name of the current group ``net view``
- Network Discovery ``net view /all``
- View all domains ``net view /domain``
- Domain forest, domain tree information
- Domain Trust Information ``nltest /domain_trusts``
- Positioning Domain Control ``net time /domain``
- View username in the domain ``dsquery user``
- Query domain group name ``net group /domain``
- Query Domain Admins ``net group "Domain Admins" /domain``
- Domain control information
- ``nltest /dclist:xx``
- ``Get-NetDomain``
- ``Get-NetDomainController``
- ``net group "Domain controllers"``
- Group Policy

User Information
----------------------------------------
- View users
- ``net user``
- ``whoami`` / ``whoami /priv`` / ``whoami /all``
- ``wmic useraccount get /ALL /format:csv``
- User Privilege Information ``whoami /priv``
- View current permissions ``net localgroup administrators``
- View online users ``quser``/ ``qwinsta``/ ``query user``
- View the current computer name, full name, user name, system version, worksite domain, login domain ``net config Workstation``
- ACL information ``get-acl``

Network information
----------------------------------------
- Intranet segment information
- Network card information ``ipconfig``
- External network export
- ARP table ``arp -a``
- Routing table ``route print``
- Listening port ``netstat -ano``
- Connected port
- Port information
- ``Get-NetTCPConnection``
- hosts file
- Main and backup DNS
- DNS cache
- ``ipconfig /displaydns``
- ``Get-CimInstance -Namespace root/StandardCimv2 -ClassName MSFT_DNSClientCache``
- Detect the network situation
- `powershell -c "1..65535 | % {echo ((new-object Net.Sockets.TcpClient).Connect('allports.exposed',$_)) $_ } 2>$null"`

Firewall
----------------------------------------
- View the firewall status ``netsh advfirewall show allprofiles``
- Firewall log directory ``netsh firewall show logging``
- Firewall rules ``netsh advfirewall firewall show rule name=all``
- ``netsh firewall show config``
- ``netsh firewall show state``

Password information
----------------------------------------
- Windows RDP connection record
- Account password saved in the browser
- Various passwords in the system password manager
- Password information in unattended installation files
- ``C:\sysprep.inf``
- ``C:\sysprep\sysprep.xml``
- ``C:\Windows\Panther\Unattend\Unattended.xml``
- ``C:\Windows\Panther\Unattended.xml``

Note information
----------------------------------------
- ``cmdkey /l``
- klist
- msf meterpreter

Special files
----------------------------------------
- document
- xlsx / xls
- docx / doc
- PPTX / PPT
- vsdx / vsd
- md / txt
- Compressed files
- zip / rar / 7z
- VPN configuration
- OVPn
- Code
- py / php / jsp / aspx / asp / sql
- Configuration File
- conf / ini / xml
- Specific keywords
- Account / Account / Login / User
- Password / pass
- Code/Document/Shift/Backup/git/svn
- Email / Address Book / Cluster / Office
- Agent / Intranet / VPN
- Equipment/Assets
- System / Operation / Topology / Network / IT
- Backend / Admin / Database
- Monitoring / Isolation / Firewall / Gate Gate / Patrol Inspection

LAN surviving host
----------------------------------------
- NetBIOS Scan
- OXID Scan

other
----------------------------------------
- Shared folders enabled
- Recycling yard
- Recently run commands
- Access file history
- Check the patch installation status
- ``wmic qfe get Caption,Description,HotFixID,InstalledOn``
- Logs and Event Information
- `` Wevtutil```
- ``eventvwr``
- Registration Information
- ``reg``
- Various agent monitoring software installed
- Installed antivirus software
- View/Set suffix association
- ``assoc``
- ``assoc .ext=example``
- PowerShell Version
- .Net version
- Wi-Fi Password
