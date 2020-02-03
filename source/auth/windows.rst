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

Hash
----------------------------------------

LM Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LM Hash(LAN Manager Hash) 是windows最早用的加密算法，由IBM设计。LM Hash 使用硬编码秘钥的DES，且存在缺陷。早期的Windows系统如XP、Server 2003等使用LM Hash，而后的系统默认禁用了LM Hash并使用NTLM Hash。

在LM Hash中，用户的密码会转换为大写，最长14字节，不足14字节则需要在其后添加0×00补足14字节。而后将14字节分为两段7字节的密码，通过处理得到两组8字节数据。而后以 ``KGS!@#$%`` 作为秘钥对这两组数据进行标准DES加密，拼接后得到最后的LM Hash。

NT Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
为了解决LM Hash的安全问题，微软于1993年在Windows NT 3.1中引入了NTLM协议。将密码统一转换为unicode编码后计算md4 Hash，得到NT Hash。

参考链接
----------------------------------------
- `Windows身份认证及利用思路 <https://www.freebuf.com/articles/system/224171.html>`_
