Information collection
========================================

basic commands
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
- View the installed driver ``DRIVERQUERY``
- View operating system information
    - Architecture ``wmic os get osarchitecture``
    - System name ``wmic os get caption``
- View the logical disk ``wmic logicaldisk get caption``
- View installed software information ``wmic product get name,version``
- View service information
    - ``wmic service list brief``
    - ``sc query``
    - ``Get-WmiObject win32_service | select PathName``

domain information
----------------------------------------
- Get the computer name of the current group ``net view``
- Network discovery ``net view /all``
- View all domains ``net view /domain``
- Domain forest and domain tree information
- Domain trust information ``nltest /domain_trusts``
- Locate domain control ``net time /domain``
- View usernames in the domain ``dsquery user``
- Query domain group name ``net group /domain``
- Query domain administrators ``net group "Domain Admins" /domain``
- Domain control information
    - ``nltest /dclist:xx``
    - ``Get-NetDomain``
    - ``Get-NetDomainController``
    - ``net group "Domain controllers"``
- Group Policy

User information
----------------------------------------
- View users
    - ``net user``
    - ``whoami`` / ``whoami /priv`` / ``whoami /all``
    - ``wmic useraccount get /ALL /format:csv``
- User privilege information ``whoami /priv``
- View current permissions ``net localgroup administrators``
- View online users ``quser`` / ``qwinsta`` / ``query user``
- View the current computer name, full name, user name, system version, workstation domain, login domain ``net config Workstation``
- ACL information ``get-acl``

Network information
----------------------------------------
-Intranet segment information
- Network card information ``ipconfig``
- External network export
- ARP table ``arp -a``
- Routing table ``route print``
- Listening port ``netstat -ano``
- Connected port
- Port information
    - ``Get-NetTCPConnection``
- hosts file
- Primary and backup DNS
- DNS cache
    - ``ipconfig /displaydns``
    - ``Get-CimInstance -Namespace root/StandardCimv2 -ClassName MSFT_DNSClientCache``
- Detect outgoing network conditions
    - `powershell -c "1..65535 | % {echo ((new-object Net.Sockets.TcpClient).Connect('allports.exposed',$_)) $_ } 2>$null"`

firewall
----------------------------------------
- View firewall status ``netsh advfirewall show allprofiles``
- Firewall log directory ``netsh firewall show logging``
- Firewall rules ``netsh advfirewall firewall show rule name=all``
- ``netsh firewall show config``
- ``netsh firewall show state``

Password information
----------------------------------------
- Windows RDP connection logging
- Account password saved in the browser
- Various passwords in system password manager
- Password information in unattended installation files
    - ``C:\sysprep.inf``
    - ``C:\sysprep\sysprep.xml``
    - ``C:\Windows\Panther\Unattend\Unattended.xml``
    - ``C:\Windows\Panther\Unattended.xml``

Bill information
----------------------------------------
- ``cmdkey /l``
- klist
- msf meterpreter

special files
----------------------------------------
- document
    - xlsx / xls
    - docx / doc
    - pptx / ppt
    - vsdx / vsd
    - md / txt
- compressed files
    - zip / rar / 7z
-VPN configuration
    - ovpn
- code
    - py / php / jsp / aspx / asp / sql
- Configuration file
    - conf / ini / xml
- specific keywords
    - account / account / login / login / user
    - Password / pass
    - code/documentation/handover/backup/git/svn
    - Email/Address Book/Cluster/Office
    - Proxy/Intranet/VPN
    - Equipment/Assets
    - System / Operation and Maintenance / Topology / Network / IT
    - Backend/Administrator/Database
    - Monitoring / Isolation / Firewall / Gatekeeper / Inspection

LAN survival host
----------------------------------------
- NetBIOS scan
- OXID scan

other
----------------------------------------
- Enabled shared folders
- Recycle Bin
- Recently run commands
- Access file history
- Check patch installation status
    - ``wmic qfe get Caption,Description,HotFixID,InstalledOn``
- Logs and event information
    - ``wevtutil``
    - ``eventvwr``
- Registry information
    - ``reg``
- Various types of agent monitoring software installed
- Installed anti-virus software
- View/set suffix associations
    - ``assoc``
    - ``assoc .ext=example``
- PowerShell version
- .Net version
- Wi-Fi password
