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
- `SharpSploit <https://github.com/cobbr/SharpSploit>`_ .NET post-exploitation library written in C#
- `SharpBeacon <https://github.com/mai1zhi2/SharpBeacon>`_ 用.net重写了CobaltStrike stager及Beacon，其中包括正常上线、文件管理、进程管理、令牌管理、结合SysCall进行注入、原生端口转发、关ETW等一系列功能
- `Koadic <https://github.com/zerosum0x0/koadic>`_ is a Windows post-exploitation rootkit

隐藏
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `ProcessHider <https://github.com/M00nRise/ProcessHider>`_ Post-exploitation tool for hiding processes from monitoring applications
- `Invoke Phant0m <https://github.com/hlldz/Invoke-Phant0m>`_ Windows Event Log Killer
- `EventCleaner <https://github.com/QAX-A-Team/EventCleaner>`_ A tool mainly to erase specified records from Windows event logs, with additional functionalities

DLL注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `sRDI <https://github.com/monoxgas/sRDI>`_ Shellcode Reflective DLL Injection

rootkit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `r77-rootkit <https://github.com/bytecode77/r77-rootkit>`_ Ring 3 rootkit with single file installer and fileless persistence that hides processes, files, network connections, etc

伪造
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `parent PID spoofing <https://github.com/countercept/ppid-spoofing>`_ Scripts for performing and detecting parent PID spoofing
- `GetSystem <https://github.com/py7hagoras/GetSystem>`_ This is a C# implementation of making a process/executable run as NT AUTHORITY/SYSTEM. This is achieved through parent ID spoofing of almost any SYSTEM process.

MiTM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Seth <https://github.com/SySS-Research/Seth>`_ Perform a MitM attack and extract clear text credentials from RDP connections
- `pyrdp <https://github.com/GoSecure/pyrdp>`_ RDP man-in-the-middle (mitm) and library for Python with the ability to watch connections live or after the fact

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
- `traitor <https://github.com/liamg/traitor>`_ Automatic Linux privesc via exploitation of low-hanging fruit e.g. gtfobins, pwnkit, dirty pipe, +w docker.sock

rootkit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `rootkit <https://github.com/nurupo/rootkit>`_
- `Diamorphine <https://github.com/m0nad/Diamorphine>`_ LKM rootkit for Linux Kernels 2.6.x/3.x/4.x/5.x (x86/x86_64 and ARM64) 

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
- `SecretScanner <https://github.com/deepfence/SecretScanner>`_ Find secrets and passwords in container images and file systems

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
- `Cooolis-ms <https://github.com/Rvn0xsy/Cooolis-ms>`_ 包含了Metasploit Payload Loader、Cobalt Strike External C2 Loader、Reflective DLL injection的代码执行工具

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
