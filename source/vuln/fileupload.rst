File upload
========================================

File type detection bypass
----------------------------------------

Change request bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some sites only detect file types on the front end, and this type of detection can directly modify network requests bypass.
Similarly, some sites only check the information in the HTTP Header on the backend, such as ``Content-Type``, etc., and this kind of check can also be bypassed by modifying network requests.

Magic detection bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some sites use file headers to detect file types, and this kind of check can be added to the corresponding bytes before the shell to bypass the check. The header bytes of several common file types are shown in the following table

==============      ============================
Type Binary value
==============      ============================
JPG                 FF D8 FF E0 00 10 4A 46 49 46
GIF                 47 49 46 38 39 61
PNG 89 50 47
Spectrum 49 49 A 00
BMP                 42 4D
==============      ============================

Suffix bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some services only judge file types based on suffixes, information during uploading, or Magic Header, and can be bypassed at this time.

php Due to historical reasons, some interpreters may support suffixes that comply with the regular ``/ph(p[2-7]?|t(ml)?)/``, such as ``php``/``php5``/ ``pht`` / ``phtml`` / ``shtml`` / ``pwml`` / ``phtm`` etc. can test this type when uploading php files is prohibited.

The jsp engine may parse suffixes such as ``jspx``/`jspf``/`jspa``/`jsw``/`jsv``/`jtml``. Asp supports ``asa` `/ ``asax`` / ``cer`` / ``cdx`` / ``aspx`` / ``ascx`` / ``ashx`` / ``asmx`` / ``asp{80- 90}`` and other suffixes.

In addition to these bypasses, other suffixes can also cause problems, such as ``vbs`` / ``asis`` / ``sh`` / ``reg`` / ``cgi`` / ``exe`` / ``dll`` / ``com`` / ``bat`` / ``pl`` / ``cfc`` / ``cfm`` / ``ini`` etc.

System naming bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
On Windows systems, uploading ``index.php.` will be renamed to ``.``, and suffix checking can be bypassed.
You can also try ``index.php%20`, ``index.php:1.jpg``````````, etc.
In Linux systems, you can try uploading a file named ``index.php/.`` or ``./aa/../index.php/.``

.user.ini
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During the execution of php, in addition to the main php.ini, PHP will also scan the INI file in each directory, starting from the directory where the executed PHP file is located and continues to the web root directory ($_SERVER[ 'DOCUMENT_ROOT'] specified). If the executed PHP file is outside the web root directory, only that directory is scanned. ``.user.ini`` can define options for patterns other than PHP_INI_SYSTEM, so you can use ``.user.ini`` to add non-php suffix files to construct a shell, such as ``auto_prepend_file=01.gif` ` .

WAF bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some wafs only process part of the data during the writing process, and can bypass their processing functions by adding a large amount of junk data.

In addition, Waf and Web systems handle ``boundary`` inconsistently, so you can use the wrong ``boundary`` to complete the bypass.

Competition upload bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some servers use the method of saving first and then deleting illegal files. In this kind of server, you can upload a file that will generate a Web shell and try to access it. After multiple times, you can get the shell.

Attack skills
----------------------------------------

Apache rewrites GetShell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache can consider uploading.htaccess based on whether redirects are allowed

The content is

::

AddType application/x-httpd-php .png
php_flag engine 1

You can use png or other suffix files to make php scripts

Read files at will with soft links
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When the uploaded compressed package file will be decompressed, you can consider uploading files with symbolic links.
If the server is not protected properly, the effect of reading any file can be achieved.

Protection skills
----------------------------------------
- Use whitelist to limit the types of uploaded files
- Use stricter file type checking methods
- Restrict Web Server to parse uploaded folders

Reference link
----------------------------------------
- `Constructing a high-quality upload vulnerability Fuzz dictionary <https://www.freebuf.com/articles/web/188464.html>`_
