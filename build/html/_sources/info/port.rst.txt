Port information
========================================

Common ports and their fragility points
----------------------------------------
- FTP (21/TCP)
- Default username and password ``anonymous:anonymous``
- Brute force password cracking
- VSFTP version backdoor
- SSH (22/TCP)
- Some versions of SSH have vulnerabilities to enumerate user names
- Brute force password cracking
- Telent (23/TCP)
- Brute force password cracking
- Sniffing and grab plaintext password
- SMTP (25/TCP)
- The sender can be forged without authentication
- DNS (53/UDP & 53/TCP)
- Domain Transmission Vulnerability
- DNS hijacking
- DNS cache poisoning
- DNS spoofing
- SPF / DMARC Check
- DDoS
- DNS Query Flood
- DNS rebound
- DNS tunnel
- DHCP 67/68
- Hijacking/deception
- TFTP (69/TCP)
- HTTP (80/TCP)
- Kerberos (88/TCP)
- Mainly used to listen to KDC ticket requests
- Forged gold and silver notes
- POP3 (110/TCP & 995/TCP)
- Blast
- RPC (135/TCP)
- wmic service utilization
- NetBIOS (137/UDP & 138/UDP)
- Unauthorized access
- Weak password
- NetBIOS / Samba (139/TCP)
- Unauthorized access
- Weak password
- IMAP (143/TCP & 993/TCP)
- SNMP (161/TCP & 161/UDP)
- Public Weak Password
- LDAP (389/TCP)
- Used for permission verification services on domains
- Anonymous access
- Injection
- HTTPS (443/TCP)
- SMB (445/TCP)
- Windows protocol cluster, the main function is file sharing service
- ``net use \192.168.1.1 /user:xxx\username password``
- Linux Rexec (512/TCP & 513/TCP & 514/TCP)
- Weak password
- Rsync (873/TCP)
- Unauthorized access
- RPC (1025/TCP)
- NFS anonymous access
- Java RMI (1090/TCP & 1099/TCP)
- Deserialization remote command execution vulnerability
- MSSQL (1433/TCP)
- Weak password
- Differential Backup GetShell
- SA escalation of rights
- Oracle (1521/TCP)
- Weak password
- NFS (2049/TCP)
- Improper permission settings
- ``showmount <host>``
- ZooKeeper (2171/TCP & 2375/TCP)
- No identity authentication
- Docker Remote API (2375/TCP)
- IP not restricted / TLS authentication not enabled
- ``http://docker.addr:2375/version``
- MySQL (3306/TCP)
- Weak password
- Log writing WebShell
- UDF escalation
- MOF escalation
- RDP / Terminal Services (3389/TCP)
- Weak password
- Postgres (5432/TCP)
- Weak password
- Execute system commands
- VNC (5900/TCP)
- Weak password
- CouchDB (5984/TCP)
- Unauthorized access
- WinRM (5985/TCP)
- Windows' implementation of WS-Management
- It is necessary to start manually on Vista, and the service is enabled by default in Windows Server 2008.
- Redis (6379/TCP)
- No password or weak password
- Absolute path writing WebShell
- Planned mission rebound Shell
- Write SSH public key
- Master-slave replication RCE
- Windows Write Startup Item
- Kubernetes API Server (6443/TCP && 10250/TCP)
- ``https://Kubernetes:10250/pods``
- JDWP (8000/TCP)
- Remote command execution
- ActiveMQ (8061/TCP)
- Jenkin (8080/TCP)
- Unauthorized access
- Elasticsearch (9200/TCP)
- Code execution
- ``http://es.addr:9200/_plugin/head/``
- ``http://es.addr:9200/_nodes``
- Memcached (11211/TCP & 11211/UDP)
- Unauthorized access
- RabbitMQ (15672/TCP & 15692/TCP & 25672/TCP)
- MongoDB (27017/TCP)
- No password or weak password
- Hadoop (50070/TCP & 50075/TCP)
- Unauthorized access

In addition to the possible problems listed above, if the services exposed to the public network are not the latest version, there may be vulnerabilities that have been published.

Common port scanning technology
----------------------------------------

Full scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The scan host attempts to establish a formal connection with a port of the target host using the three-time handshake. If the connection is successfully established, the port is open and vice versa.

Full scan is simple to implement and can be performed with lower permissions. But there will be a lot of obvious records in the traffic log.

Half scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Half-scan is also called SYN scan. In half-scan, only the SYN data segment is sent. If the reply is RST, the port is in the closed state. If the reply is SYN/ACK, the port is in the listening state. However, this method requires high permissions, and most firewalls have begun to process this scanning method.

FIN scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FIN scan sends a FIN packet to the target. If it is an open port, it will return the RST packet, and the closed port will not return the packet. This way, it can be used to determine whether the port is open.

This method is not in the state of TCP three-time handshake, so it will not be recorded, and it is more hidden than SYN scanning.

Web Services
----------------------------------------
- Jenkins
- Unauthorized access
- Gitlab
- Corresponding version CVE
- Zabbix
- Improper permission settings

Batch Search
----------------------------------------
- Censys
- Shodan
- ZoomEye
