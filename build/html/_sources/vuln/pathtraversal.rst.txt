Directory travel
========================================

Introduction
----------------------------------------
Directory traversal (also known as directory traversal/path traversal) is to access any files and directories stored on the file system by using directory control sequences such as ``../`` or the absolute path of the file, especially Application source code, configuration files, important system files, etc.

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
- `` \ localhost

Filter bypass
----------------------------------------
- Single replacement
- ``...//``
- URL encoding
- 16-bit Unicode encoding
- ``\u002e``
- Extra long UTF-8 encoding
- `` `` `e0% 40% no

defense
----------------------------------------
Before performing file-related APIs, user input should be filtered. Under stronger rules, whitelists can be used, only pure letters or numeric characters are allowed.

If the rules allow more characters, it is best to use the current operating system path normalize the function and then filter it, and finally make related calls.

Reference link
----------------------------------------
- `Directory traversal by portswigger <https://portswigger.net/web-security/file-path-traversal>`_
- `Path Traversal by OWASP <https://www.owasp.org/index.php/Path_Traversal>`_
- `path normalization <https://blogs.msdn.microsoft.com/jeremykuhne/2016/04/21/path-normalization/>`_
- `Breaking Parser Logic: Take Your Path Normalization Off and Pop 0days Out defcon <https://i.blackhat.com/us-18/Wed-August-8/us-18-Orange-Tsai-Breaking-Parser-Logic-Take-Your-Path-Normalization-Off-And-Pop-0days-Out-2.pdf>`_
