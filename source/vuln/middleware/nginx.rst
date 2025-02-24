Nginx
========================================

Fast-CGI Close
----------------------------------------
With Fast-CGI shutdown, Nginx still has a parsing vulnerability:
Add ``%00.php`` after the file path (xx.jpg), that is, ``xx.jpg%00.php`` will be parsed as a php file

Fast-CGI is enabled
----------------------------------------
When Fast-CGI is enabled, add ``/xx.php`` after the file path, then ``xx.jpg/xx.php`` will be parsed into a php file

CVE-2013-4547
----------------------------------------
produce

Configuration error
----------------------------------------

Directory travel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If there is a configuration like location /foo { alias /bar/; }`` in the configuration, ``/foo../`` will be parsed as ``/bar/../``, resulting in directory traversal The occurrence of

Directory traversal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When ``autoindex on`` is turned on in the configuration, a directory traversal vulnerability exists in Nginx.

Reference link
----------------------------------------
- `CVE-2013-4547 In-depth utilization and analysis of Nginx analysis vulnerabilities <http://www.91ri.org/9064.html>`_
