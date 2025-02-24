Trace cleaning
========================================

log
----------------------------------------
- View log ``eventvwr``
- Forged logs ``eventcreate``
- Operation log
- 3389 Login List
- File Open Log
- File modification log
- Browser Log
- System Events
- Program installation record
- Program Delete Records
- Program update record
- Login log
- System Security Log
- Log path
- System Log ``%SystemRoot%\System32\Winevt\Logs\System.evtx``
- Security Log ``%SystemRoot%\System32\Winevt\Logs\Security.evtx``
- Application Log ``%SystemRoot%\System32\Winevt\Logs\Application.evtx``
- Service Log
- iis `%SystemDrive%\ Inetpub \ Logs \ Log files \ W3SVC1 \` `

Registration form
----------------------------------------
- AppCompatFlags
- Background Activity Moderator (BAM)
- M UI cache
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
Pre-read folder is used to store pre-read information of files that have been accessed by the system, with the extension PF. The location is in ``C:\Windows\Prefetch``.

JumpLists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Records the recently used documents and applications by the user, so that the user can quickly jump to the specified file, located in ``%APPDATA%\Microsoft\Windows\Recent``.

Amcache / RecentFileCache.bcf
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
These two files are used in Windows to track application compatibility issues with different executables, which can be used to determine when the executable was first run and when the last modified.

In Windows 7, Windows Server 2008 R2 and other systems, the file is saved in ``C:\Windows\AppCompat\Programs\RecentFileCache.bcf``, which contains the program creation time, last modification time, last access time, and file name .

In Windows 8, Windows 10, Windows Server 2012 and other systems, the file is saved in ``C:\Windows\AppCompat\Programs\Amcache.hve``, which contains information such as file size, version, sha1, binary file type, etc.

Timeline
----------------------------------------
The Windows timeline is a new feature introduced by Windows 10 in version 1803. It records visited websites, edited documents, running programs, etc.

Delete completely
----------------------------------------
- Overwrite file multiple times ``cipher /w:<path>```
- Format D: /P:<count>```
