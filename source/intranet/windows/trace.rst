trace cleaning
========================================

log
----------------------------------------
- View log ``eventvwr``
- Fake log ``eventcreate``
- Operation log
    - 3389 login list
    - File open log
    - File modification log
    - Browser logs
    - System events
    - Program installation records
    - Program to delete records
    - Program update record
- Login log
    - System security log
- Log path
    - System log ``%SystemRoot%\System32\Winevt\Logs\System.evtx``
    - Security log ``%SystemRoot%\System32\Winevt\Logs\Security.evtx``
    - Application log ``%SystemRoot%\System32\Winevt\Logs\Application.evtx``
- Service log
    - IIS ``%SystemDrive%\inetpub\logs\LogFiles\W3SVC1\``

Registry
----------------------------------------
- AppCompatFlags
- Background Activity Moderator (BAM)
- MuiCache
- RecentApps
- RunMRU
- ShimCache (AppCompatCache)

Registry key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- HKEY_LOCAL_MACHINE\system\CurrentControlSet\Services\Eventlog

document
----------------------------------------

Prefetch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The pre-read folder is used to store pre-read information of files that have been accessed by the system. The extension is PF. The location is ``C:\Windows\Prefetch``.

JumpLists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Records the documents and applications recently used by the user, allowing the user to quickly jump to the specified file. The location is ``%APPDATA%\Microsoft\Windows\Recent``.

Amcache / RecentFileCache.bcf
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
These two files are used in Windows to track compatibility issues with applications with different executables. It can be used to determine when the executable was first run and when it was last modified.

In Windows 7, Windows Server 2008 R2 and other systems, the file is saved in ``C:\Windows\AppCompat\Programs\RecentFileCache.bcf``, including the program's creation time, last modification time, last access time and file name.

In Windows 8, Windows 10, Windows Server 2012 and other systems, the file is saved in ``C:\Windows\AppCompat\Programs\Amcache.hve``, including file size, version, sha1, binary file type and other information.

timeline
----------------------------------------
Windows Timeline is a new feature introduced in Windows 10 version 1803. It records visited websites, edited documents, running programs, etc.

Delete completely
----------------------------------------
- Overwrite the file ``cipher /w:<path>`` multiple times
- Format a disk count times ``format D: /P:<count>``
