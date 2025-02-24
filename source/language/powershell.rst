PowerShell
========================================

Execution policy
----------------------------------------
PowerShell provides six types of execution strategies: Restricted, AllSigned, RemoteSigned, Unrestricted, Bypass, and Undefined.

The Restricted policy can execute a single command, but cannot execute scripts. This policy is used by default in Windows 8 and Windows Server 2012.

The AllSigned policy allows execution of all scripts with digital signatures.

RemoteSigned When executing a script downloaded from the network, the script needs to have a digital signature, otherwise the script will not be run. If the script is created locally, it can be executed directly and does not require the script to have a digital signature.

Unrestricted This is a relatively tolerant strategy that allows unsigned scripts to be run. For scripts downloaded from the network, security prompts will be given before running.

BypassBypass execution policy does not place any restrictions on the execution of scripts. Any script can be executed and there will be no security prompts.

UndefinedUndefined means that no script policy is set, and the default script policy will be inherited or used.

Confusion
----------------------------------------
- ``-EC``
- ``-EncodedCommand``
- ``-EncodedComman``
- ``-EncodedComma``
- ``-EncodedComm``

Common features
----------------------------------------

Plan tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

$Action = New-ScheduledTaskAction -Execute "calc.exe"
$Trigger = New-ScheduledTaskTrigger -AtLogon
$User = New-ScheduledTaskPrincipal -GroupId "BUILTIN\Administrators" -RunLevel Highest
$Set = New-ScheduledTaskSettingsSet
$object = New-ScheduledTask -Action $Action -Principal $User -Trigger $Trigger -Settings $Set
Register-ScheduledTask AtomicTask -InputObject $object
Unregister-ScheduledTask -TaskName "AtomicTask" -confirm:$false

Create a link
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

$Shell = New-Object -ComObject ("WScript.Shell")
$ShortCut = $Shell.CreateShortcut("$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup	est.lnk")
$ShortCut.TargetPath="cmd.exe"
$ShortCut.WorkingDirectory = "C:\Windows\System32";
$ShortCut.WindowStyle = 1;
$ShortCut.Description = "test.";
$ShortCut.Save()

coding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

$OriginalCommand = '#{powershell_command}'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
$EncodedCommand =[Convert]::ToBase64String($Bytes)

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Alias
- ``alias``
- Download the file
- ``Invoke-WebRequest "https://example.com/test.zip" -OutFile "$env:TEMP	est.zip"``
- Decompression
- ``Expand-Archive $env:TEMP	est.zip $env:TEMP	est -Force``
- Process
- Start the process ``Start-Process calc``
- Stop the process ``Stop-Process -ID $pid``
- document
- Create a new file ``New-Item #{file_path} -Force | Out-Null``
- Set file content ``Set-Content -Path #{file_path} -Value "#{Content}"``
- Add file content ``Add-Content -Path #{file_path} -Value "#{Content}"``
- Copy file ``Copy-Item src dst``
- Delete file ``Remove-Item #{outputfile} -Force -ErrorAction Ignore``
- Subdirectory ``Get-ChildItem #{file_path}``
- Serve
- Get Service ``Get-Service -Name "#{service_name}"``
- Start the service ``Start-Service -Name "#{service_name}"``
- Stop service ``Stop-Service -Name "#{service_name}"``
- Delete service ``Remove-Service -Name "#{service_name}"``
- Get WMI support ``Get-WmiObject -list``

Reference link
----------------------------------------
- `PowerShell official document <https://docs.microsoft.com/zh-cn/powershell/>`_
