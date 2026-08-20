Port information
========================================

Common ports and their vulnerabilities
----------------------------------------
- FTP (21/TCP)
    - Default username and password ``anonymous:anonymous``
    - Brute force password cracking
    - A certain version of VSFTP backdoor
- SSH (22/TCP)
    - There is a vulnerability in some versions of SSH that can enumerate user names
    - Brute force password cracking
- Telent (23/TCP)
    - Brute force password cracking
    - Sniff and capture clear text passwords
- SMTP (25/TCP)
    - The sender can be forged without authentication
- DNS (53/UDP & 53/TCP)
    - Domain transfer vulnerability
    - DNS hijacking
    - DNS cache poisoning
    - DNS spoofing
    - SPF / DMARC Check
    - DDoS
        - DNS Query Flood
        - DNS bounce
    - DNS tunnel
- DHCP 67/68
    - Hijacking/spoofing
- TFTP (69/TCP)
- HTTP (80/TCP)
- Kerberos (88/TCP)
    - Mainly used to monitor KDC ticket requests
    - For counterfeiting of gold and silver bills
- POP3 (110/TCP & 995/TCP)
    - blast
- RPC (135/TCP)
    - wmic service utilization
- NetBIOS (137/UDP & 138/UDP)
    - Unauthorized access
    - Weak passwords
- NetBIOS / Samba (139/TCP)
    - Unauthorized access
    - Weak passwords
- IMAP (143/TCP & 993/TCP)
- SNMP (161/TCP & 161/UDP)
    - Public weak password
- LDAP (389/TCP)
    - Used for authority verification services on the domain
    - Anonymous access
    - Inject
- HTTPS (443/TCP)
- SMB (445/TCP)
    - Windows protocol cluster, the main function is file sharing service
    - ``net use \\192.168.1.1 /user:xxx\username password``
- Linux Rexec (512/TCP & 513/TCP & 514/TCP)
    - Weak passwords
- Rsync (873/TCP)
    - Unauthorized access
- RPC (1025/TCP)
    - NFS anonymous access
- Java RMI (1090/TCP & 1099/TCP)
    - Deserialization remote command execution vulnerability
- MSSQL (1433/TCP)
    - Weak password
    - Differential backup GetShell
    - SA privilege escalation
- Oracle (1521/TCP)
    - Weak password
- NFS (2049/TCP)
    - Improper permission settings
    - ``showmount <host>``
- ZooKeeper (2171/TCP & 2375/TCP)
    - No authentication
- Docker Remote API (2375/TCP)
    - No IP restrictions / TLS authentication not enabled
    - ``http://docker.addr:2375/version``
- MySQL (3306/TCP)
    - Weak password
    - Log writing WebShell
    - UDF privilege escalation
    -MOF privilege escalation
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
    - Windows implementation of WS-Management
    - It needs to be started manually on Vista. In Windows Server 2008, the service is turned on by default.
- Redis (6379/TCP)
    - No password or weak password
    - Write WebShell with absolute path
    - Scheduled task rebound Shell
    - Write SSH public key
    - Master-slave replication RCE
    - Windows write startup items
- Kubernetes API Server (6443/TCP && 10250/TCP)
    - ``https://Kubernetes:10250/pods``
- JDWP (8000/TCP)
    - Remote command execution
- ActiveMQ (8061/TCP)
- Jenkin (8080/TCP)
    - Unauthorized access
- Elasticsearch (9200/TCP)
    - code execution
    - ``http://es.addr:9200/_plugin/head/``
    - ``http://es.addr:9200/_nodes``
- Memcached (11211/TCP & 11211/UDP)
    - Unauthorized access
- RabbitMQ (15672/TCP & 15692/TCP & 25672/TCP)
- MongoDB (27017/TCP)
    - No password or weak password
- Hadoop (50070/TCP & 50075/TCP)
    - Unauthorized access

In addition to the possible problems listed above, if the services exposed on the public Internet are not the latest version, there may be vulnerabilities that have been disclosed.

Common port scanning techniques
----------------------------------------

full scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The scanning host attempts to use a three-way handshake to establish a formal connection with a port of the target host. If the connection is successfully established, the port is open, otherwise it is closed.

Full scan is simple to implement and can be performed with lower permissions. But there will be a lot of obvious records in the traffic logs.

half scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Half scan is also called SYN scan. In half scan, only the SYN data segment is sent. If the response is RST, the port is in the closed state. If the response is SYN/ACK, the port is in the listening state. However, this method requires higher permissions, and most of the current firewalls have begun to process this scanning method.

FIN scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FIN scanning sends a FIN packet to the target. If it is an open port, an RST packet will be returned. If the port is closed, no data packet will be returned. This way you can determine whether the port is open.

This method is not in the state of TCP three-way handshake, so it will not be recorded. It is more covert than SYN scanning.

Web services
----------------------------------------
- Jenkins
    - Unauthorized access
- Gitlab
    - Corresponding version CVE
- Zabbix
    - Improper permission settings

Batch search
----------------------------------------
- Censys
- Shodan
- ZoomEye
