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

常见功能
----------------------------------------

计划任务
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

    $Action = New-ScheduledTaskAction -Execute "calc.exe"
    $Trigger = New-ScheduledTaskTrigger -AtLogon
    $User = New-ScheduledTaskPrincipal -GroupId "BUILTIN\Administrators" -RunLevel Highest
    $Set = New-ScheduledTaskSettingsSet
    $object = New-ScheduledTask -Action $Action -Principal $User -Trigger $Trigger -Settings $Set
    Register-ScheduledTask AtomicTask -InputObject $object
    Unregister-ScheduledTask -TaskName "AtomicTask" -confirm:$false

创建链接
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

    $Shell = New-Object -ComObject ("WScript.Shell")
    $ShortCut = $Shell.CreateShortcut("$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup\test.lnk")
    $ShortCut.TargetPath="cmd.exe"
    $ShortCut.WorkingDirectory = "C:\Windows\System32";
    $ShortCut.WindowStyle = 1;
    $ShortCut.Description = "test.";
    $ShortCut.Save()

编码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

    $OriginalCommand = '#{powershell_command}'
    $Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
    $EncodedCommand =[Convert]::ToBase64String($Bytes)

其他
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 别名
    - ``alias``
- 下载文件
    - ``Invoke-WebRequest "https://example.com/test.zip" -OutFile "$env:TEMP\test.zip"``
- 解压缩
    - ``Expand-Archive $env:TEMP\test.zip $env:TEMP\test -Force``
- 进程
    - 启动进程 ``Start-Process calc``
    - 停止进程 ``Stop-Process -ID $pid``
- 文件
    - 新建文件 ``New-Item #{file_path} -Force | Out-Null``
    - 设置文件内容 ``Set-Content -Path #{file_path} -Value "#{Content}"``
    - 追加文件内容 ``Add-Content -Path #{file_path} -Value "#{Content}"``
    - 复制文件 ``Copy-Item src dst``
    - 删除文件 ``Remove-Item #{outputfile} -Force -ErrorAction Ignore``
    - 子目录 ``Get-ChildItem #{file_path}``
- 服务
    - 获取服务 ``Get-Service -Name "#{service_name}"``
    - 启动服务 ``Start-Service -Name "#{service_name}"``
    - 停止服务 ``Stop-Service -Name "#{service_name}"``
    - 删除服务 ``Remove-Service -Name "#{service_name}"``
- 获取WMI支持 ``Get-WmiObject -list``

参考链接
----------------------------------------
- `PowerShell 官方文档 <https://docs.microsoft.com/zh-cn/powershell/>`_
