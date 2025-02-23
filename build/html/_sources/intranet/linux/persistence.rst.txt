Endurance
========================================

Elevate permissions
----------------------------------------
- Kernel exploit
- Attacking services with root privileges
- Use third-party services to raise rights
- Through an executable file with SUID attribute
- Find executable files that may be elevated
- ``find / -perm +4000 -ls``
- ``find / -perm -u=s -type f 2>/dev/null``
- ``find / -user root -perm -4000 -print 2>/dev/null``
- ``find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null``
- Take advantage of available root permissions
- `` sudo -l``
- Take advantage of misconfigured crontab tasks

Self-start
----------------------------------------
- /etc/init.d
- /etc/rc.d/rc.local
- ~/.bashrc
- ~/.zshrc

back door
----------------------------------------
- ssh backdoor
- ``alias ssh='strace -o /tmp/.ssh.log -e read,write,connect -s 2048 ssh'``
- Backdoor Account
- Common applications
- ICMP
- DNS
- icmp backdoor
- Backdoor port reuse
- ``.``` Hide file at the beginning
- rootkit
