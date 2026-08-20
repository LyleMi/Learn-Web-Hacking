Nginx
========================================

Fast-CGI off
----------------------------------------
With Fast-CGI turned off, Nginx still has a parsing vulnerability:
Add ``%00.php`` after the file path (xx.jpg), that is, ``xx.jpg%00.php`` will be parsed as a php file

Fast-CGI on
----------------------------------------
When Fast-CGI is turned on, add ``/xx.php`` after the file path, then ``xx.jpg/xx.php`` will be parsed as a php file

CVE-2013-4547
----------------------------------------
``a.jpg\x20\x00.php``

Configuration error
----------------------------------------

directory traversal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If there is a configuration similar to ``location /foo { alias /bar/; }`` in the configuration, ``/foo../`` will be parsed into ``/bar/../``, causing directory traversal to occur.

directory traversal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There is a directory traversal vulnerability in Nginx when ``autoindex on`` is turned on in the configuration.

Reference link
----------------------------------------
- `CVE-2013-4547 In-depth utilization and analysis of Nginx parsing vulnerability <http://www.91ri.org/9064.html>`_
