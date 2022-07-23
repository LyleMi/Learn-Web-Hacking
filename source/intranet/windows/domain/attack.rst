攻击类型
========================================

黄金票据利用
----------------------------------------
在认证过程中，经过client与AS的通信会得到TGT，黄金票据（Golden Ticket）就是伪造票据授予票据（TGT），也被称为认证票据。

黄金票据利用需要与DC通信，且需要获取krbtgt的hash，但是可以获取任何Kerbose服务权限。

白银票据利用
----------------------------------------
白银票据（Silver Tickets）伪造利用的是Kerberos认证中的第三个步骤，在第三步的时候，client会带着ticket向server的某个服务进行请求，如果验证通过就可以访问server上的指定服务了，这里的ticket是基于client info、server session key、end time、server hash。这里client info已知，end time可以构造，server session key是TGS生成的，所以只要server的NTLM hash即可。银票伪造的是TGS，只能访问指定的服务。

DCSync 攻击
----------------------------------------
域内有多台域控服务器时，为了同步域控服务器的修改，微软提供了基于远程目录协议 `DRSR <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47>`_ 的同步机制。

在多个域控服务器之间，每隔一段时间会有一次域数据的同步。由需要同步的域控服务器向其它服务器发送 GetNCChanges 请求，请求中包含需要同步的数据。数据量较多时，则重复这个过程。

DCSync 就是使用这种机制进行域渗透的技术，由Benjamin DELPY gentilkiwi和Vincent LE TOUX共同编写，在2015年添加到 mimikatz 的一个功能，可以导出域内所有用户的hash。

这种方式需要满足以下任一一种权限：

- Administrators 组内的用户
- Domain Admins 组内的用户
- Enterprise Admins 组内的用户
- 域控制器的计算机帐户

或者拥有特定的几条 DACL:

- DS-Replication-Get-Changes
- DS-Replication-Get-Changes-All
- DS-Replication-Get-Changes-In-Filtered-Set

当没有管理员用户，但是拥有 WriteDACL 权限时，可以写入上述 DACL 来完成 DCSync 。

对于这种攻击，可以通过检测 GetNCChanges 发起者的方式，如果由非域控机器发起对应请求，则可以认为是 DCSync 攻击。

DCShadow 攻击
----------------------------------------
DCShadow是由来自法国的安全研究人员Benjamin Delpy和Vincent Le Toux在2018年的微软蓝帽（Blue Hat）大会上提出。

DCShadow攻击指在Active Directory环境下创建一个恶意的域控制器，并用它来推送恶意对象。

哈希传递攻击
----------------------------------------
哈希传递攻击（Pass-the-Hash，PTH）是通过传递NTLM哈希来认证的攻击方法，常用的工具有mimikatz等。

票据传递攻击
----------------------------------------
票据传递攻击（Pass-the-Ticket Attacks，PtT）是一种使用Kerberos票据代替明文密码或NTLM哈希的方法。PtT最常见的用途可能是使用黄金票据和白银票据，通过PtT访问主机相当简单。

Kerberoasting Attacks
----------------------------------------
Kerberoasting攻击由Tim Medin在2014 DerbyCon conference上 `公开 <https://www.youtube.com/watch?v=PUyhlN-E5MU>`_ 。指域内的任何一台主机，都可以通过查询SPN，Kerberoasting即是向域内的所有服务请求TGS，然后进行暴力破解。

Roasting AS-REP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
该攻击枚举域中不需要Kerberos预身份认证的帐户，向这些账户请求一条加密信息，并离线尝试获取到的账户哈希。该方式需要账户明确设置了 ``DONT_REQ_PREAUTH`` 。

Kerberos Delegation Attacks
----------------------------------------
在一个域中，A使用Kerberos身份验证访问服务B，B再使用A的身份去访问C，这个过程就可以理解为委派。委派主要分为非约束委派（Unconstrained delegation）和约束委派（Constrained delegation）两种，非约束委派可以访问域内任意其它服务，约束委派对认证做了限制不可以访问其他的服务。

Kerberos Delegation（Kerberos委派）攻击分为非约束委派攻击和约束委派攻击。原理都是基于域内已经配置了委派的账户来获取其它账户的权限。

其他漏洞利用
----------------------------------------
- 域用户提权 (CVE-2022-26923)
- KDC bamboozling (CVE-2021-42287)
- Name impersonation (CVE-2021-42278)
- ProxyShell (CVE-2021-34473)
- ProxyLogon (CVE-2021-26855)
- PrintNightmare (CVE-2021-1675 / CVE-2021-34527)
- SMBGhost (CVE-2020-0796)
- Zerologon (CVE-2020-1472)
- NTLM Relay (CVE-2019-1040)
- 永恒之蓝 (MS17-010)
- 域用户提权 (MS14-068)
- Gpp漏洞 (MS14-025)
- SAMR协议漏洞 (MS14-016)
