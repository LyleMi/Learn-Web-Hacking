PowerShell
========================================

执行策略
----------------------------------------
PowerShell 提供了 Restricted、AllSigned、RemoteSigned、Unrestricted、Bypass、Undefined 六种类型的执行策略。

Restricted 策略可以执行单个的命令，但是不能执行脚本，Windows 8、 Windows Server 2012中默认使用该策略。

AllSigned 策略允许执行所有具有数字签名的脚本。

RemoteSigned 当执行从网络上下载的脚本时，需要脚本具有数字签名，否则不会运行这个脚本。如果是在本地创建的脚本则可以直接执行，不要求脚本具有数字签名。

Unrestricted 这是一种比较宽容的策略，允许运行未签名的脚本。对于从网络上下载的脚本，在运行前会进行安全性提示。

BypassBypass 执行策略对脚本的执行不设任何的限制，任何脚本都可以执行，并且不会有安全性提示。

UndefinedUndefined 表示没有设置脚本策略，会继承或使用默认的脚本策略。

混淆
----------------------------------------
- ``-EC``
- ``-EncodedCommand``
- ``-EncodedComman``
- ``-EncodedComma``
- ``-EncodedComm``

参考链接
----------------------------------------
- `PowerShell 官方文档 <https://docs.microsoft.com/zh-cn/powershell/>`_
