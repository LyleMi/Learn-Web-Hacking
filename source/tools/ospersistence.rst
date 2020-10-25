操作系统持久化
========================================

Windows
----------------------------------------

凭证获取 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `mimikatz <https://github.com/gentilkiwi/mimikatz>`_
- `RdpThief <https://github.com/0x09AL/RdpThief>`_ Extracting Clear Text Passwords from mstsc.exe using API Hooking
- `quarkspwdump <https://github.com/quarkslab/quarkspwdump>`_ Dump various types of Windows credentials without injecting in any process
- `SharpDump <https://github.com/GhostPack/SharpDump>`_ C# port of PowerSploit's Out-Minidump.ps1 functionality

权限提升
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `WindowsExploits <https://github.com/abatchy17/WindowsExploits>`_
- `GTFOBins <https://github.com/GTFOBins/GTFOBins.github.io>`_ Curated list of Unix binaries that can be exploited to bypass system security restrictions
- `JAWS <https://github.com/411Hall/JAWS>`_ Just Another Windows (Enum) Script

UAC Bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `WinPwnage <https://github.com/rootm0s/WinPwnage>`_ UAC bypass, Elevate, Persistence and Execution methods
- `UACME <https://github.com/hfiref0x/UACME>`_ Defeating Windows User Account Control
- `UAC Bypass In The Wild <https://github.com/sailay1996/UAC_Bypass_In_The_Wild>`_

免杀
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `SigThief <https://github.com/secretsquirrel/SigThief>`_ Stealing Signatures and Making One Invalid Signature at a Time

C2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Koadic <https://github.com/zerosum0x0/koadic>`_ is a Windows post-exploitation rootkit

隐藏
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `ProcessHider <https://github.com/M00nRise/ProcessHider>`_ Post-exploitation tool for hiding processes from monitoring applications
- `Invoke Phant0m <https://github.com/hlldz/Invoke-Phant0m>`_ Windows Event Log Killer
- `EventCleaner <https://github.com/QAX-A-Team/EventCleaner>`_ A tool mainly to erase specified records from Windows event logs, with additional functionalities

伪造
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `parent PID spoofing <https://github.com/countercept/ppid-spoofing>`_ Scripts for performing and detecting parent PID spoofing
- `GetSystem <https://github.com/py7hagoras/GetSystem>`_ This is a C# implementation of making a process/executable run as NT AUTHORITY/SYSTEM. This is achieved through parent ID spoofing of almost any SYSTEM process.

综合工具
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Nishang <https://github.com/samratashok/nishang>`_ Offensive PowerShell for red team, penetration testing and offensive security

Linux
----------------------------------------

权限提升
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `linux exploit suggester <https://github.com/mzet-/linux-exploit-suggester>`_
- `LinEnum <https://github.com/rebootuser/LinEnum>`_ Scripted Local Linux Enumeration & Privilege Escalation Checks
- `AutoLocalPrivilegeEscalation <https://github.com/ngalongc/AutoLocalPrivilegeEscalation>`_

rootkit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `rootkit <https://github.com/nurupo/rootkit>`_

后门
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `prism <https://github.com/andreafabrizi/prism>`_ is an user space stealth reverse shell backdoor
- `icmpsh <https://github.com/inquisb/icmpsh>`_ Simple reverse ICMP shell

综合
----------------------------------------

凭证获取 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `sshLooterC <https://github.com/mthbernardes/sshLooterC>`_ program to steal passwords from ssh
- `keychaindump <https://github.com/juuso/keychaindump>`_ A proof-of-concept tool for reading OS X keychain passwords
- `LaZagne <https://github.com/AlessandroZ/LaZagne>`_ Credentials recovery project

权限提升
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `BeRoot <https://github.com/AlessandroZ/BeRoot>`_ Privilege Escalation Project - Windows / Linux / Mac

RAT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `QuasarRAT <https://github.com/quasar/QuasarRAT>`_

C2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Empire <https://github.com/EmpireProject/Empire>`_
- `pupy <https://github.com/n1nj4sec/pupy>`_
- `Covenant <https://github.com/cobbr/Covenant>`_ is a collaborative .NET C2 framework for red teamers

DNS Shell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `DNS Shell <https://github.com/sensepost/DNS-Shell>`_ DNS-Shell is an interactive Shell over DNS channel
- `Reverse DNS Shell <https://github.com/ahhh/Reverse_DNS_Shell>`_ A python reverse shell that uses DNS as the c2 channel

Cobalt Strike
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Cobalt Strike <https://www.cobaltstrike.com>`_
- `CrossC2 <https://github.com/gloxec/CrossC2>`_ generate CobaltStrike's cross-platform payload
- `Cobalt Strike Aggressor Scripts <https://github.com/timwhitez/Cobalt-Strike-Aggressor-Scripts>`_

日志清除
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Log killer <https://github.com/Rizer0/Log-killer>`_ Clear all logs in [linux/windows] servers

Botnet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `byob <https://github.com/malwaredllc/byob>`_ Build Your Own Botnet

免杀工具
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `AV Evasion Tool <https://github.com/1y0n/AV_Evasion_Tool>`_ 掩日 - 免杀执行器生成工具
- `DKMC <https://github.com/Mr-Un1k0d3r/DKMC>`_ Dont kill my cat - Malicious payload evasion tool
