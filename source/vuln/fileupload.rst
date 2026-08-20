File upload
========================================

File type detection bypass
----------------------------------------

Change request bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some sites only detect file types on the front end. This type of detection can be bypassed by directly modifying the network request.
Similarly, some sites only check the information in the HTTP Header on the backend, such as ``Content-Type``, etc. This check can also be bypassed by modifying the network request.

Magic detection bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some sites use file headers to detect file types. This check can be done by adding corresponding bytes before the shell to bypass the check. The header bytes of several common file types are shown in the following table

==============      ============================
type binary value
==============      ============================
JPG                 FF D8 FF E0 00 10 4A 46 49 46
GIF                 47 49 46 38 39 61
PNG                 89 50 4E 47
TIF                 49 49 2A 00
BMP                 42 4D
==============      ============================

suffix bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some services only determine the file type based on the suffix, information when uploading, or Magic Header, which can be bypassed in this case.

Due to historical reasons, some php interpreters may support suffixes that conform to the regular pattern ``/ph(p[2-7]?|t(ml)?)/``, such as ``php`` / ``php5`` / ``pht`` / ``phtml`` / ``shtml`` / ``pwml`` / ``phtm``, etc. This type can be tested when uploading php files is prohibited.

The jsp engine may parse ``jspx`` / ``jspf`` / ``jspa`` / ``jsw`` / ``jsv`` / ``jtml`` and other suffixes, asp supports ``asa`` / ``asax`` / ``cer`` / ``cdx`` / ``aspx`` / ``ascx`` / ``ashx`` / ``asmx`` / ``asp{80-90}`` etc. suffix.

In addition to these bypasses, other suffixes may also cause problems, such as ``vbs`` / ``asis`` / ``sh`` / ``reg`` / ``cgi`` / ``exe`` / ``dll`` / ``com`` / ``bat`` / ``pl`` / ``cfc`` / ``cfm`` / ``ini``, etc.

System naming bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In Windows systems, uploading ``index.php.`` will be renamed to ``.``, which can bypass the suffix check.
You can also try ``index.php%20``, ``index.php:1.jpg`` ``index.php::$DATA``, etc.
In Linux systems, you can try uploading a file named ``index.php/.`` or ``./aa/../index.php/.``

.user.ini
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During the execution of php, in addition to the main ``php.ini``, PHP will also scan INI files in each directory, starting from the directory where the executed PHP file is located and going up to the web root directory (specified by $_SERVER['DOCUMENT_ROOT']). If the PHP file being executed is outside the web root directory, only that directory will be scanned. ``.user.ini`` can define options for modes other than PHP_INI_SYSTEM, so you can use ``.user.ini`` plus a file with a non-php suffix to construct a shell, such as ``auto_prepend_file=01.gif``.

WAF bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some wafs only process part of the data for performance reasons during the writing process. In this case, you can bypass its processing function by adding a large amount of garbage data.

In addition, the processing of ``boundary`` by Waf and the web system is inconsistent, and the wrong ``boundary`` can be used to complete the bypass.

Competing upload bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some servers adopt the method of first saving and then deleting illegal files. In this kind of server, you can repeatedly upload a file that will generate a Web Shell and try to access it. After several times, you can get the Shell.

Attack skills
----------------------------------------

Apache rewrites GetShell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache may consider uploading .htaccess based on whether redirects are allowed

The content is

::

    AddType application/x-httpd-php .png
    php_flag engine 1

You can use png or other suffix files to make php scripts

Soft link to read files arbitrarily
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When uploading a compressed package file that will be decompressed, you can consider uploading a file containing a symbolic link.
If the server is not well protected, the effect of reading any file can be achieved

Protective skills
----------------------------------------
- Use whitelists to limit the types of uploaded files
- Use stricter file type checking
- Limit Web Server's parsing of uploaded folders

Reference link
----------------------------------------
- `Construct high-quality upload vulnerability Fuzz dictionary <https://www.freebuf.com/articles/web/188464.html>`_
