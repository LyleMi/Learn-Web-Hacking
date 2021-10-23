信息收集
========================================

基本命令
----------------------------------------
- 主机名 ``hostname``
- 查询所有计算机名称 ``dsquery computer``
- 查看配置及补丁信息
    - ``systeminfo``
    - ``wmic qfe get description,installedOn /format:csv``
- 查看版本 ``ver``
- 进程信息
    - ``tasklist /svc``
    - ``wmic process get caption,executablepath,commandline /format:csv``
    - ``get-process``
- 查看所有环境变量 ``set``
- 查看计划任务 ``schtasks /QUERY /fo LIST /v``
- 查看安装驱动 ``DRIVERQUERY``
- 查看操作系统信息
    - 架构 ``wmic os get osarchitecture``
    - 系统名 ``wmic os get caption``
- 查看逻辑盘 ``wmic logicaldisk get caption``
- 查看安装的软件信息 ``wmic product get name,version``
- 查看服务信息
    - ``wmic service list brief``
    - ``sc query``
    - ``Get-WmiObject win32_service | select PathName``

域信息
----------------------------------------
- 获取当前组的计算机名 ``net view``
- 网络发现  ``net view /all``
- 查看所有域 ``net view /domain``
- 域森林、域树信息
- 域信任信息 ``nltest /domain_trusts``
- 定位域控 ``net time /domain``
- 查看域中的用户名 ``dsquery user``
- 查询域组名称 ``net group /domain``
- 查询域管理员 ``net group "Domain Admins" /domain``
- 域控信息
    - ``nltest /dclist:xx``
    - ``Get-NetDomain``
    - ``Get-NetDomainController``
    - ``net group "Domain controllers"``
- 组策略

用户信息
----------------------------------------
- 查看用户 
    - ``net user``
    - ``whoami`` / ``whoami /priv`` / ``whoami /all``
    - ``wmic useraccount get /ALL /format:csv``
- 用户特权信息 ``whoami /priv``
- 查看当前权限 ``net localgroup administrators``
- 查看在线用户 ``quser`` / ``qwinsta`` / ``query user``
- 查看当前计算机名，全名，用户名，系统版本，工作 站域，登陆域 ``net config Workstation``
- ACL 信息 ``get-acl``

网络信息
----------------------------------------
- 内网网段信息
- 网卡信息 ``ipconfig``
- 外网出口
- ARP表 ``arp -a``
- 路由表 ``route print``
- 监听的端口 ``netstat -ano``
- 连接的端口
- 端口信息
    - ``Get-NetTCPConnection``
- hosts文件
- 主备 DNS
- DNS缓存
    - ``ipconfig /displaydns``
    - ``Get-CimInstance -Namespace root/StandardCimv2 -ClassName MSFT_DNSClientCache``
- 探测出网情况
    - `powershell -c "1..65535 | % {echo ((new-object Net.Sockets.TcpClient).Connect('allports.exposed',$_)) $_ } 2>$null"`

防火墙
----------------------------------------
- 查看防火墙状态 ``netsh advfirewall show allprofiles``
- 防火墙日志目录 ``netsh firewall show logging``
- 防火墙规则 ``netsh advfirewall firewall show rule name=all``
- ``netsh firewall show config``
- ``netsh firewall show state``

密码信息
----------------------------------------
- Windows RDP连接记录
- 浏览器中保存的账号密码
- 系统密码管理器中的各种密码
- 无人值守安装文件中的密码信息
    - ``C:\sysprep.inf``
    - ``C:\sysprep\sysprep.xml``
    - ``C:\Windows\Panther\Unattend\Unattended.xml``
    - ``C:\Windows\Panther\Unattended.xml``

票据信息
----------------------------------------
- ``cmdkey /l``
- klist
- msf meterpreter

特殊文件
----------------------------------------
- 文档
    - xlsx / xls
    - docx / doc
    - pptx / ppt
    - vsdx / vsd
    - md / txt
- 压缩文件
    - zip / rar / 7z
- VPN配置
    - ovpn
- 代码
    - py / php / jsp / aspx / asp / sql
- 配置文件
    - conf / ini / xml
- 特定关键字
    - 账号 / 账户 / 登录 / login / user
    - 密码 / pass
    - 代码 / 文档 / 交接 / 备份 / git / svn
    - 邮箱 / 通讯录 / 集群 / 办公
    - 代理 / 内网 / VPN
    - 设备 / 资产
    - 系统 / 运维 / 拓扑 / 网络 / IT
    - 后台 / 管理员 / 数据库
    - 监控 / 隔离 / 防火墙 / 网闸 / 巡检

局域网存活主机
----------------------------------------
- NetBIOS扫描
- OXID扫描

其他
----------------------------------------
- 启用的共享文件夹
- 回收站
- 最近运行的命令
- 访问文件历史记录
- 查看补丁安装情况
    - ``wmic qfe get Caption,Description,HotFixID,InstalledOn``
- 日志与事件信息
    - ``wevtutil``
    - ``eventvwr``
- 注册表信息
    - ``reg``
- 安装的各类 agent 监控软件
- 安装的杀毒软件
- 查看/设置后缀关联
    - ``assoc``
    - ``assoc .ext=example``
- PowerShell 版本
- .Net 版本
- Wi-Fi 密码
