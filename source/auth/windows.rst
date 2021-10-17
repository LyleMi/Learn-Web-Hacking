Windows
========================================

本地用户认证
----------------------------------------
Windows 在进行本地登录认证时操作系统会使用用户输入的密码作为凭证去与系统中的密码进行对比验证。通过 ``winlogon.exe`` 接收用户输入传递至 ``lsass.exe`` 进行认证。

``winlogon.exe`` 用于在用户注销、重启、锁屏后显示登录界面。 ``lsass.exe`` 用于将明文密码变成NTLM Hash的形式与SAM数据库比较认证。

SAM
----------------------------------------
安全帐户管理器(Security Accounts Manager，SAM) 是Windows操作系统管理用户帐户的安全所使用的一种机制。用来存储Windows操作系统密码的数据库文件为了避免明文密码泄漏SAM文件中保存的是明文密码在经过一系列算法处理过的 Hash值被保存的Hash分为LM Hash、NTLM Hash。当用户进行身份认证时会将输入的Hash值与SAM文件中保存的Hash值进行对比。

SAM文件保存于 ``%SystemRoot%\system32\config\sam`` 中，在注册表中保存在 ``HKEY_LOCAL_MACHINE\SAM\SAM`` ， ``HKEY_LOCAL_MACHINE\SECURITY\SAM`` 。 在正常情况下 SAM 文件处于锁定状态不可直接访问、复制、移动仅有 system 用户权限才可以读写该文件。

密码破解
----------------------------------------
- 通过物理接触主机、启动其他操作系统来获取 Windows 分区上的 ``%SystemRoot%\system32\config\sam`` 文件
- 获取 ``%SystemRoot%\repair\sam._`` 文件。
- 使用工具从注册表中导出SAM散列值
- 从网络中嗅探分析SMB报文，从中获取密码散列

SPNEGO
----------------------------------------
SPNEGO (SPNEGO: Simple and Protected GSS-API Negotiation)是微软提供的一种使用GSS-API认证机制的安全协议，用于使Webserver共享Windows Credentials，它扩展了Kerberos。
