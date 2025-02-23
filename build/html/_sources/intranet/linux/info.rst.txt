Information collection
========================================

Get kernel, operating system and device information
----------------------------------------
- Version Information
- ``uname -a`` All versions
- ``uname -r`` kernel version information
- ``uname -n`` system host name
- ``uname -m`` Linux kernel architecture
- Kernel information ``cat /proc/version``
- CPU information ``cat /proc/cpuinfo``
- Publish information
- ``cat /etc/*-release``
- ``cat /etc/issue``
- Hostname ``hostname``
- File system ``df -a``
- Kernel log ``dmesg``/``/var/log/dmesg``

Users and Groups
----------------------------------------
- List all users of the system ``cat /etc/passwd``
- List all groups in the system ``cat /etc/group``
- List all users hash(root)``cat /etc/shadow```
- User
- Query user's basic information ``finger``
- Currently logged in user ``users```` who -a````/var/log/utmp``
- Query user without password ``grep 'x:0:' /etc/passwd``
- Currently logged in user ``w````
- Logged in user information ``last`` / ``/var/log/wtmp``
- Display the last login information of all users in the system ``lastlog`` / ``/var/log/lastlog``
- Login success log ``/var/log/secure``
- Login failure log ``/var/log/faillog``
- View privileged user ``grep :0 /etc/passwd``
- Check the last modified time of passwd ``ls -l /etc/passwd``
- Check if there is an empty password user ``awk -F: 'length($2)==0 {print $1}' /etc/shadow``
- View remote login account ``awk '/\$1|\$6/{print $1}' /etc/shadow``
- View users with sudo permissions
- ``cat /etc/sudoers | grep -v "^#\|^$" | grep "ALL=(ALL)"``

User and permission information
----------------------------------------
- Current user ``whoami``
- Current user information ``id``
- Users who can be promoted to root with sudo ``cat /etc/sudoers``
- List the instructions that are currently executable and unexecutable by users ``sudo -l``

Environmental information
----------------------------------------
- Print system environment information ``env``
- Print system environment information ``set``
- Path information in environment variables ``echo $PATH``
- Print history command ``history`` / ``~/.bash_history``
- Show current path ``pwd``
- Show default system traversal ``cat /etc/profile``
- Show available shells ``cat /etc/shells``

Process information
----------------------------------------
- View process information ``ps aux``
- Resource possession status ``top -c``
- View process association file ``lsof -c $PID``
- Complete command line information ``/proc/$PID/cmdline``
- Process command name ``/proc/$PID/comm``
- Symbol link to the current working directory of the process ``/proc/$PID/cwd``
- Symbol link to run the program ``/proc/$PID/exe``
- Process environment variable ``/proc/$PID/environ``
- The situation when the process opens the file ``/proc/$PID/fd``

Service Information
----------------------------------------
- List of services managed by inetd ``cat /etc/inetd.conf``
- List of services managed by xinetd ``cat /etc/xinetd.conf``
- nfs server configuration ``cat /etc/exports````
- Email information ``/var/log/maillog``
- ssh configuration ``sshd_config```

Plan tasks
----------------------------------------
- Displays the scheduled job (root) of the specified user ``crontab -l -u %user%``
- Plan tasks
- ``/Var/Spool/Cron/*``
- ``/where/spool/anacron/*``
- ``/etc/crontab``
- ``/etc/anacrontab``
- ``/etc/cron.*``
- ``/etc/anacrontab``
- Start-up item
- ``/etc/rc.d/init.d/``

Networking, routing and communication
----------------------------------------
- List network interface information ``/sbin/ifconfig -a`` / ``ip addr show``
- List network interface information ``cat /etc/network/interfaces``
- View system arp table ``arp -a``
- Print routing information ``route`` / ``ip ro show``
- View dns configuration information ``cat /etc/resolv.conf``
- Print local port open information ``netstat -an``
- List the configuration rules for iptable ``iptables -L``
- View port service map ``cat /etc/services``
- Hostname ``hostname -f``
- Check the process port status ``netstat -anltp | grep $PID``

Installed program
----------------------------------------
- ``rpm -qa --last`` Redhat
- ``yum list | grep installed`` CentOS
- `` ls -l/etc/yum.repos.d/``
- ``dpkg -l`` Debian
- ``cat /etc/apt/sources.list`` Debian APT
- ``pkg_info`` xBSD
- ``pkginfo`` Solaris
- ``pacman -Q`` Arch Linux
- ``emerge`` Gentoo

document
----------------------------------------
- Files for the last five days ``find / -ctime +1 -ctime -5``
- File system details ``debugfs``

Public and private key information
----------------------------------------
- ``~/.ssh``
- ``/etc/ssh``

log
----------------------------------------
- ``/var/log/boot.log``
- ``/where/log/cron``
- ``/VAR/Log/Faillog``
- ``/was/log/load log``
- ``/VAR/Log/Messages``
- ``/var/log/secure``
- ``/VAR/LOG/SYSLOG``
- ``/VAR/LOG/SYSLOG``
- ``/VAR/LOG/WTMP``
- ``/VAR/LOG/WTMP``
- ``/was/Run/UTMP``

Virtual environment detection
----------------------------------------
- ``lsmod | grep -i "vboxsf\|vboxguest"``
- Ch HRSMOD | Grep -and "VMV_Balothy | Vmxnet"
- ``lsmod | grep -i "xen-vbd\|xen-vnif"``
- ``lsmod | grep -i "virtio_pci\|virtio_net"``
- `` LMOD | grip -i "HV_VMBUS \ | HV_BLKVSC \ | HV_NETVSC \ | HV_UTILS \ | HV_STORVSC" `` ``

Information collection in container
----------------------------------------
- ``capsh --print``
- ``cat /proc/1/cgroup``
- `` Env | grabbed cube```
- ``ls -l .dockerenv``
- `` ls -l/run/secrets/kbernetes.io/``
- ``mount``
- `` ps to the
