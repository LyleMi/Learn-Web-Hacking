目录穿越
========================================

简介
----------------------------------------
目录穿越（也被称为目录遍历/directory traversal/path traversal）是通过使用 ``../`` 等目录控制序列或者文件的绝对路径来访问存储在文件系统上的任意文件和目录，特别是应用程序源代码、配置文件、重要的系统文件等。

攻击载荷
----------------------------------------

URL参数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``../``
- ``..\``
- ``..;/``

Nginx Off by Slash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``https://vuln.site.com/files../``

UNC Bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``\\localhost\c$\windows\win.ini``

过滤绕过
----------------------------------------
- 单次替换
    - ``...//``
- URL编码
- 16位Unicode编码
    - ``\u002e``
- 超长UTF-8编码
    - ``\%e0%40%ae``

防御
----------------------------------------
在进行文件操作相关的API前，应该对用户输入做过滤。较强的规则下可以使用白名单，仅允许纯字母或数字字符等。

若规则允许的字符较多，最好使用当前操作系统路径规范化函数规范化路径后，进行过滤，最后再进行相关调用。

参考链接
----------------------------------------
- `Directory traversal by portswigger <https://portswigger.net/web-security/file-path-traversal>`_
- `Path Traversal by OWASP <https://www.owasp.org/index.php/Path_Traversal>`_
- `path normalization <https://blogs.msdn.microsoft.com/jeremykuhne/2016/04/21/path-normalization/>`_
- `Breaking Parser Logic: Take Your Path Normalization Off and Pop 0days Out defcon <https://i.blackhat.com/us-18/Wed-August-8/us-18-Orange-Tsai-Breaking-Parser-Logic-Take-Your-Path-Normalization-Off-And-Pop-0days-Out-2.pdf>`_
