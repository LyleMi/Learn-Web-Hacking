directory traversal
========================================

Introduction
----------------------------------------
Directory traversal (also known as directory traversal/directory traversal/path traversal) is to access any files and directories stored on the file system, especially application source code, configuration files, important system files, etc., by using directory control sequences such as ``../`` or the absolute path of the file.

Attack payload
----------------------------------------

URL parameters
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

filter bypass
----------------------------------------
- Single replacement
    - ``...//``
- URL encoding
- 16-bit Unicode encoding
    - ``\u002e``
- Extra long UTF-8 encoding
    - ``\%e0%40%ae``

defense
----------------------------------------
Before performing APIs related to file operations, user input should be filtered. A whitelist can be used under stronger rules, allowing only pure alphabetic or numeric characters, etc.

If the rule allows a lot of characters, it is best to use the current operating system path normalization function to normalize the path, filter it, and finally make relevant calls.

Reference link
----------------------------------------
- `Directory traversal by portswigger <https://portswigger.net/web-security/file-path-traversal>`_
- `Path Traversal by OWASP <https://www.owasp.org/index.php/Path_Traversal>`_
- `path normalization <https://blogs.msdn.microsoft.com/jeremykuhne/2016/04/21/path-normalization/>`_
- `Breaking Parser Logic: Take Your Path Normalization Off and Pop 0days Out defcon <https://i.blackhat.com/us-18/Wed-August-8/us-18-Orange-Tsai-Breaking-Parser-Logic-Take-Your-Path-Normalization-Off-And-Pop-0days-Out-2.pdf>`_
