backdoor technology
========================================

development technology
----------------------------------------
- Management and control function implementation technology
    - System management: View basic system information, process management, service management
    - File management: copy/paste files, delete files/directories, download/upload files, etc.
    - Shell management
    - Keystroke logging monitoring
    - Screen capture
    - Audio monitoring
    - Video surveillance
    - View private information
    - Dynamic monitoring of removable disks
    - Remote uninstall
- Self-starting technology
    - Windows starts automatically
        - Self-start based on Windows startup directory
        - Registry-based auto-start
        - Self-starting based on service program
        - Self-starting based on ActiveX control
        - Auto-start based on scheduled tasks (Scheduled Tasks)
    -Linux self-starting
- User mode process hiding technology
    - Process hiding based on DLL insertion
        - Remote thread creation technology
        - Set window hook (HOOK) technology
    - Process hiding based on SvcHost shared service
    - Process memory replacement
- Data penetration and evasion technology
    - Bounce port
    - Protocol tunnel
        - HTTP
        - MSN
        - Google Talk
- Kernel-level hidden technology (Rootkit)
- Disk boot-level hidden technology (Bootkit)
    - MBR
    - BIOS
    - NTLDR
    - boot.ini
- Restore software countermeasures technology

Backdoor to avoid killing
----------------------------------------
- Traditional static code detection
    - Packing
    - Added flower command
    - Input form to avoid killing
- Heuristic code detection
    - Dynamic function calls
- Cloud scanning and killing
    - Dynamically increase its own size
    - Change the domain name resolution address of the cloud scanning and killing server
    - disconnection
    - Use hash collision to bypass cloud "whitelisting"
- Attack the main anti-virus software
    - Change system time
    - Window message attack
    - Actively send IRP to control the main defense driver
- Utilize certificate trust
    - Steal and exploit legitimate certificates
    - Forging certificates using hash collisions
    - Using legitimate programs to solve the problem of DLL hijacking

Detection technology
----------------------------------------
- Detection based on self-start information
- Detection based on process information
- Detection based on data transmission
- Rootkit/Bootkit detection

Backdoor analysis
----------------------------------------
- Dynamic analysis
- static analysis
    - Anti-virus engine scan
    - File format recognition
    - File packing identification and unpacking
    - Plain text string search
    - Analysis of link libraries and import/export functions
