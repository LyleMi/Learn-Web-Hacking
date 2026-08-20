Information collection
========================================

Get kernel, operating system and device information
----------------------------------------
- version information
    - ``uname -a`` all versions
    - ``uname -r`` Kernel version information
    - ``uname -n`` system host name
    - ``uname -m`` Linux kernel architecture
- Kernel information ``cat /proc/version``
- CPU information ``cat /proc/cpuinfo``
- Publish information
    - ``cat /etc/*-release``
    - ``cat /etc/issue``
- Hostname ``hostname``
- file system ``df -a``
- Kernel log ``dmesg`` / ``/var/log/dmesg``

Users and groups
----------------------------------------
- List all users on the system ``cat /etc/passwd``
- List all groups in the system ``cat /etc/group``
- List all user hashes (root) ``cat /etc/shadow``
- User
    - Query the user's basic information ``finger``
    - Currently logged in users ``users`` ``who -a`` ``/var/log/utmp``
    - Query passwordless users ``grep 'x:0:' /etc/passwd``
- Currently logged in user ``w``
- Logged-in user information ``last`` / ``/var/log/wtmp``
- Display the latest login information of all users in the system ``lastlog`` / ``/var/log/lastlog``
- Login success log ``/var/log/secure``
- Login failure log ``/var/log/faillog``
- View privileged users ``grep :0 /etc/passwd``
- Check the last modification time of passwd ``ls -l /etc/passwd``
- Check if there is a user with an empty password ``awk -F: 'length($2)==0 {print $1}' /etc/shadow``
- Check the remote login account ``awk '/\$1|\$6/{print $1}' /etc/shadow``
- View users with sudo privileges
    - ``cat /etc/sudoers | grep -v "^#\|^$" | grep "ALL=(ALL)"``

User and permission information
----------------------------------------
- Current user ``whoami``
- Current user information ``id``
- Users who can be elevated to root using sudo (root) ``cat /etc/sudoers``
- List the commands that the current user can and cannot execute ``sudo -l``

environmental information
----------------------------------------
- Print system environment information ``env``
- Print system environment information ``set``
- Path information in environment variables ``echo $PATH``
- Print history command ``history`` / ``~/.bash_history``
- Display current path ``pwd``
- Show default system traversal ``cat /etc/profile``
- Show available shells ``cat /etc/shells``

process information
----------------------------------------
- View process information ``ps aux``
- Resource occupancy ``top -c``
- View process associated files ``lsof -c $PID``
- Complete command line information ``/proc/$PID/cmdline``
- The command name of the process ``/proc/$PID/comm``
- Symbolic link to the current working directory of the process ``/proc/$PID/cwd``
- Symbolic link to run the program ``/proc/$PID/exe``
- Process environment variables ``/proc/$PID/environ``
- When a process opens a file ``/proc/$PID/fd``

Service information
----------------------------------------
- List of services managed by inetd ``cat /etc/inetd.conf``
- List of services managed by xinetd ``cat /etc/xinetd.conf``
- nfs server configuration ``cat /etc/exports``
- Mail information ``/var/log/mailog``
- ssh configuration ``sshd_config``

Scheduled tasks
----------------------------------------
- Display scheduled jobs for the specified user (root) ``crontab -l -u %user%``
- Schedule tasks
    - ``/var/spool/cron/*``
    - ``/var/spool/anacron/*``
    - ``/etc/crontab``
    - ``/etc/anacrontab``
    - ``/etc/cron.*``
    - ``/etc/anacrontab``
- Startup items
    - ``/etc/rc.d/init.d/``

Networking, routing and communications
----------------------------------------
- List network interface information ``/sbin/ifconfig -a`` / ``ip addr show``
- List network interface information ``cat /etc/network/interfaces``
- View the system arp table ``arp -a``
- Print routing information ``route`` / ``ip ro show``
- View dns configuration information ``cat /etc/resolv.conf``
- Print local port open information ``netstat -an``
- List iptable configuration rules ``iptables -L``
- View port service mapping ``cat /etc/services``
- Hostname ``hostname -f``
- Check the process port status ``netstat -anltp | grep $PID``

Installed program
----------------------------------------
- ``rpm -qa --last`` Redhat
- ``yum list | grep installed`` CentOS
- ``ls -l /etc/yum.repos.d/``
- ``dpkg -l`` Debian
- ``cat /etc/apt/sources.list`` Debian APT
- ``pkg_info`` xBSD
- ``pkginfo`` Solaris
- ``pacman -Q`` Arch Linux
- ``emerge`` Gentoo

document
----------------------------------------
- Files in the last five days ``find / -ctime +1 -ctime -5``
- File system details ``debugfs``

Public and private key information
----------------------------------------
- ``~/.ssh``
- ``/etc/ssh``

log
----------------------------------------
- ``/var/log/boot.log``
- ``/var/log/cron``
- ``/var/log/faillog``
- ``/var/log/lastlog``
- ``/var/log/messages``
- ``/var/log/secure``
- ``/var/log/syslog``
- ``/var/log/syslog``
- ``/var/log/wtmp``
- ``/var/log/wtmp``
- ``/var/run/utmp``

Virtual environment detection
----------------------------------------
- ``lsmod | grep -i "vboxsf\|vboxguest"``
- ``lsmod | grep -i "vmw_baloon\|vmxnet"``
- ``lsmod | grep -i "xen-vbd\|xen-vnif"``
- ``lsmod | grep -i "virtio_pci\|virtio_net"``
- ``lsmod | grep -i "hv_vmbus\|hv_blkvsc\|hv_netvsc\|hv_utils\|hv_storvsc"``

Collection of information within the container
----------------------------------------
- ``capsh --print``
- ``cat /proc/1/cgroup``
- ``env | grep KUBE``
- ``ls -l .dockerenv``
- ``ls -l /run/secrets/Kubernetes.io/``
- ``mount``
- ``ps aux``
