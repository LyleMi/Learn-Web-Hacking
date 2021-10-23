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
DCSync是域渗透中经常会用到的技术。DCSync是mimikatz在2015年添加的一个功能，由Benjamin DELPY gentilkiwi和Vincent LE TOUX共同编写，基于 `DRS <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47>`_ 来导出域内所有用户的hash。

这种方式需要满足以下任一一种权限：

- Administrators组内的用户
- Domain Admins组内的用户
- Enterprise Admins组内的用户
- 域控制器的计算机帐户

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
- ProxyLogon (CVE-2021-26855)
- ProxyShell (CVE-2021-34473)
- SMBGhost (CVE-2020-0796)
- Zerologon (CVE-2020-1472)
- 永恒之蓝 (MS17-010)
