PowerShell
========================================

execution strategy
----------------------------------------
PowerShell provides six types of execution policies: Restricted, AllSigned, RemoteSigned, Unrestricted, Bypass, and Undefined.

The Restricted policy can execute a single command, but cannot execute scripts. This policy is used by default in Windows 8 and Windows Server 2012.

The AllSigned policy allows execution of all digitally signed scripts.

RemoteSigned When executing a script downloaded from the Internet, the script needs to be digitally signed, otherwise the script will not run. If the script is created locally, it can be executed directly, and the script is not required to have a digital signature.

Unrestricted This is a more permissive policy that allows unsigned scripts to run. For scripts downloaded from the Internet, a security prompt will appear before running.

The BypassBypass execution policy does not place any restrictions on the execution of scripts. Any script can be executed without security prompts.

UndefinedUndefined means that no script policy is set, and the default script policy will be inherited or used.

Confuse
----------------------------------------
- ``-EC``
- ``-EncodedCommand``
- ``-EncodedComman``
- ``-EncodedComma``
- ``-EncodedComm``

Common functions
----------------------------------------

Scheduled tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

    $Action = New-ScheduledTaskAction -Execute "calc.exe"
    $Trigger = New-ScheduledTaskTrigger -AtLogon
    $User = New-ScheduledTaskPrincipal -GroupId "BUILTIN\Administrators" -RunLevel Highest
    $Set = New-ScheduledTaskSettingsSet
    $object = New-ScheduledTask -Action $Action -Principal $User -Trigger $Trigger -Settings $Set
    Register-ScheduledTask AtomicTask -InputObject $object
    Unregister-ScheduledTask -TaskName "AtomicTask" -confirm:$false

Create link
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: powershell

    $Shell = New-Object -ComObject ("WScript.Shell")
    $ShortCut = $Shell.CreateShortcut("$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup\test.lnk")
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
- Download files
    - ``Invoke-WebRequest "https://example.com/test.zip" -OutFile "$env:TEMP\test.zip"``
- Unzip
    - ``Expand-Archive $env:TEMP\test.zip $env:TEMP\test -Force``
- process
    - Start the process ``Start-Process calc``
    - Stop the process ``Stop-Process -ID $pid``
- document
    - New file ``New-Item #{file_path} -Force | Out-Null``
    - Set file content ``Set-Content -Path #{file_path} -Value "#{Content}"``
    -Append file content ``Add-Content -Path #{file_path} -Value "#{Content}"``
    - Copy file ``Copy-Item src dst``
    - Delete files ``Remove-Item #{outputfile} -Force -ErrorAction Ignore``
    - Subdirectory ``Get-ChildItem #{file_path}``
- Serve
    - Get the service ``Get-Service -Name "#{service_name}"``
    - Start the service ``Start-Service -Name "#{service_name}"``
    - Stop the service ``Stop-Service -Name "#{service_name}"``
    - Remove service ``Remove-Service -Name "#{service_name}"``
- Get WMI support ``Get-WmiObject -list``

Reference link
----------------------------------------
- `PowerShell official documentation <https://docs.microsoft.com/zh-cn/powershell/>`_
