域渗透
========================================

Active Directory
----------------------------------------
活动目录（Active Directory，AD）是面向Windows Server的目录服务。Active Directory存储了有关网络对象的信息，并且让管理员和用户能够查找和使用这些信息。

ADDS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Active Directory提供目录服务的组件被称作Active Directory域服务（Active Directory Domain Services, ADDS），负责目录数据库的存储、增删改查等工作，可以用在多种局域网、广域网的场景中。

名称空间
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
名称空间（namespace）是一块界定好的区域，在区域内可以用名称找到与之相关的信息。

对象与属性
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ADDS内的资源都是以对象（Object）的形式存在的，对象通过属性（Attrbute）来描述其特征。

域
----------------------------------------
域指将网络中多台计算机逻辑上组织到一起，进行集中管理的逻辑环境。域是组织与存储资源的核心管理单元，在域中，至少有一台域控制器，域控制器中保存着整个域的用户帐号和安全数据库。

域树
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
域树（Trees）由多个域组成，这些域共享同一表结构和配置，形成一个连续的命名空间（namespace）。 

林
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
林（Forests）是一个复杂的AD实例，由一个或数个域组成，每个域树都有自己唯一的名称空间。

信任
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
两个域之间需要创建信任关系，才可以访问对应域内的资源。

域控制器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ADDS的目录存储在域控制器内，一个域内可以有多台域控制器，每一个域控制器的地位几乎是平等的，有几乎相同的数据库。

在一台域控制器添加一个用户账户后，这个账户会被自动复制到其他域控制器的数据库中。

AD数据库有多主机复制模式（Multi-master Replication Model）和单主机复制模式（Sing-master Replication Model）。

多主机模式可以直接更新任何一台域控制器内的AD对象，并将更新之后的对象复制到其他域控制器，大部分数据都是用多主机模式进行复制。

单主机复制模式是指由一台被称作操作主机（Operations Master）的域控制器负责接收更改数据的请求，并将数据复制到其他的域控制器。

域信任类型
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Active Directory的信任方式可以分为以下几种：

- Tree-Root Trust
    - 双向具有转移性
- Parent-Child Trust
    - 具有转移性，双向行人
- Forest Trust
    - 如果两个林创建了信任关系，则林中所有的域都相互信任
    - 两个林之间的信任关系无法自动扩展到其他林上
- Realm Trust
    - ADDS域可以和非Windows系统的Kerberos域之间创建信任
- External Trust
    - 位于两个林内的域之间可以通过外部信任来创建信任关系
- Shortcut Trust
    - 可以缩短验证用户身份的时间

攻击类型
----------------------------------------

黄金票据利用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在认证过程中，经过client与AS的通信会得到TGT，黄金票据（Golden Ticket）就是伪造票据授予票据（TGT），也被称为认证票据。

黄金票据利用需要与DC通信，且需要获取krbtgt的hash，但是可以获取任何Kerbose服务权限。

白银票据利用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
白银票据（Silver Tickets）伪造利用的是Kerberos认证中的第三个步骤，在第三步的时候，client会带着ticket向server的某个服务进行请求，如果验证通过就可以访问server上的指定服务了，这里的ticket是基于client info、server session key、end time、server hash。这里client info已知，end time可以构造，server session key是TGS生成的，所以只要server的NTLM hash即可。银票伪造的是TGS，只能访问指定的服务。

DCSync 攻击
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DCSync是域渗透中经常会用到的技术。DCSync是mimikatz在2015年添加的一个功能，由Benjamin DELPY gentilkiwi和Vincent LE TOUX共同编写，基于 `DRS <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47>`_ 来导出域内所有用户的hash。

这种方式需要满足以下任一一种权限：

- Administrators组内的用户
- Domain Admins组内的用户
- Enterprise Admins组内的用户
- 域控制器的计算机帐户

DCShadow 攻击
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DCShadow是由来自法国的安全研究人员Benjamin Delpy和Vincent Le Toux在2018年的微软蓝帽（Blue Hat）大会上提出。

DCShadow攻击指在Active Directory环境下创建一个恶意的域控制器，并用它来推送恶意对象。

票据传递攻击
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
票据传递攻击（Pass-the-Ticket Attacks，PtT）是一种使用Kerberos票据代替明文密码或NTLM哈希的方法。PtT最常见的用途可能是使用黄金票据和白银票据，通过PtT访问主机相当简单。

Kerberoasting Attacks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
域内的任何一台主机，都可以通过查询SPN，Kerberoasting即是向域内的所有服务请求TGS，然后进行暴力破解。

Kerberos Delegation Attacks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在一个域中，A使用Kerberos身份验证访问服务B，B再使用A的身份去访问C，这个过程就可以理解为委派。委派主要分为非约束委派（Unconstrained delegation）和约束委派（Constrained delegation）两种，非约束委派可以访问域内任意其它服务，约束委派对认证做了限制不可以访问其他的服务。

Kerberos Delegation（Kerberos委派）攻击分为非约束委派攻击和约束委派攻击。原理都是基于域内已经配置了委派的账户来获取其它账户的权限。
