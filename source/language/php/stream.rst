PHP Streaming
========================================

Introduction
----------------------------------------
The concept of Streams was introduced in PHP 4.3. It is an abstraction of streaming data and is used to unify data operations, such as file data, network data, compressed data, etc.

The stream can be passed through file, open, fwrite, fclose, file_get_contents,
Function operations such as file_put_contents.

Packaging protocol
----------------------------------------
PHP comes with many built-in URL-style encapsulation protocols that can be used for file system functions like fopen(), copy(), file_exists(), and filesize(). Supported protocols are available for viewing ``stream_get_wrappers().

- ``file://`` access to the local file system
- ``http://`` access HTTP(s) URL
- ``ftp://`` access to FTP(s) URLs
- ``php://`` access to individual input/output streams (I/O streams)
- ``zlib://`` compressed stream
- ``data://`` data (RFC 2397)
- ``glob://`` Find matching file path pattern
- ``phar://`` PHP Archive
- ``ssh2://`` Secure Shell 2
- `` RAR: // `` RAR
- ``ogg://`` Audio Streaming
- ``expect://`` handles interactive streams

PHP supports streaming
----------------------------------------
PHP provides some input/output (IO) streams that allow access to PHP's input/output streams, standard input/output and error descriptors, temporary file streams for in-memory and disk backups, and other filters that can operate on read and write file resources. .

It should be noted that streams are not restricted by ````````````, ``php://stdin``, ``php://memory`` and ``php: //temp`` is limited by ``````` .

Input and Output Stream
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://stdin``, ``php://stdout`` and ``php://stderr`` allow direct access to the corresponding input or output streams of the PHP process. The data stream references the copied file descriptor, so if you open ``php://stdin`` and close it afterwards, just close the copy, the STDIN that is actually referenced is not affected.

where `php://stdin` is read-only, `php://stdout`` and `php://stderr`` are write-only.

fd
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
php://fd allows direct access to the specified file descriptor. For example, ``php://fd/3`` refers to file descriptor 3.

memory与temp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://memory`` and ``php://temp`` are data streams similar to file wrappers that allow temporary data to be read and written. The only difference between the two is that `php://memory` always stores data in memory, while `php://temp`` will store after the amount of memory reaches the predefined limit (default is 2MB) Enter the temporary file. The decision on the location of the temporary file is consistent with the ``sys_get_temp_dir()``.

The memory limit of ``php://temp`` can be controlled by adding ``/maxmemory:NN``, which is the maximum amount of data retained in memory in units of bytes, and if it exceeds it, a temporary file will be used.

input
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://input`` is a read-only stream that can access the requested raw data. In case of POST requests, it is best to use ``php://input`` instead of ``$HTTP_RAW_POST_DATA`` because it does not depend on the specific php.ini directive. Moreover, in this case ``$HTTP_RAW_POST_DATA`` is not populated by default, potentially requiring less memory than Activating ``always_populate_raw_post_data`. ````````````` is invalid when ``````````.

filter
----------------------------------------
``php://filter`` is a meta wrapper designed for filtering applications when data streams are opened. PHP provides some stream filters by default, in addition to this, various custom filters can be used.

The filter has three parameters: resource, read, and write, and the resource parameter is required. It specifies the data stream you want to filter. read and write are optional parameters that can set one or more filter names, separated by pipe characters (|).

Filter list
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You can get the registered filter list through ``stream_get_filters()`. Among them, the built-in filters of PHP are as follows:

- String filter
- string.rot13
- string.toupper
- string.tolower
- string.strip_tags
- Convert filter
- convert.base64-encode
- convert.base64-decode
- convert.quoted-printable-encode
- convert.quoted-printable-decode
- convert.iconv.*
- Compression filter
- zlib.deflate
- zlib.inflate
- bzip2.compress
- bzip2.decompress
- Encryption filter
- mcrypt.``ciphername``
- mdecrypt.``ciphername``

Filters utilize tricks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- life
- ``php://filter/convert.base64-encode/resource=index.php``
- XXE will parse and report errors when reading files, and can be encoded at base64
- Base64 encoding will discard characters that are not in the code table and can be used to bypass some file formats
- Some converts will consume a lot of resources and can be used as DoS
- rot13/convert convert to WAF
