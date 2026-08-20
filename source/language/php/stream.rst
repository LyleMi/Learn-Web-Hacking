PHP stream
========================================

Introduction
----------------------------------------
The concept of streams was introduced in PHP 4.3. It is an abstraction of streaming data and is used to unify data operations, such as file data, network data, compressed data, etc.

Streams can be passed through file, open, fwrite, fclose, file_get_contents,
File_put_contents and other function operations.

encapsulation protocol
----------------------------------------
PHP comes with many built-in URL-style wrapper protocols for file system functions like fopen(), copy(), file_exists(), and filesize(). Supported protocols can be viewed with ``stream_get_wrappers()``.

- ``file://`` access the local file system
- ``http://`` access HTTP(s) URL
- ``ftp://`` to access FTP(s) URLs
- ``php://`` accesses various input/output streams (I/O streams)
- ``zlib://`` compressed stream
- ``data://`` data (RFC 2397)
- ``glob://`` finds matching file path patterns
- ``phar://`` PHP archive
- ``ssh2://`` Secure Shell 2
- ``rar://`` RAR
- ``ogg://`` audio streaming
- ``expect://`` handles interactive streams

PHP supports streams
----------------------------------------
PHP provides a number of input/output (IO) streams that allow access to PHP's input and output streams, standard input and output and error descriptors, temporary file streams in memory and disk backup, and filters that can operate on other read and write file resources.

Note that streams are not restricted by ``allow_url_fopen``, but ``php://input``, ``php://stdin``, ``php://memory`` and ``php://temp`` are restricted by ``allow_url_include``.

Input and output streams
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://stdin``, ``php://stdout`` and ``php://stderr`` allow direct access to the corresponding input or output streams of the PHP process. The data stream references the copied file descriptor, so if you open php://stdin and then close it, you only close the copy and the actual referenced STDIN is not affected.

Among them, ``php://stdin`` is read-only, ``php://stdout`` and ``php://stderr`` are write-only.

fd
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
php://fd allows direct access to the specified file descriptor. For example, ``php://fd/3`` refers to file descriptor 3.

memory and temp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://memory`` and ``php://temp`` is a file wrapper-like data stream that allows temporary data to be read and written. The only difference between the two is that php://memory always stores data in memory, while php://temp will store data in a temporary file after the amount of memory reaches a predefined limit (default is 2MB). The temporary file location is determined in the same manner as ``sys_get_temp_dir()``.

The memory limit of ``php://temp`` can be controlled by adding ``/maxmemory:NN``. NN is the maximum amount of data in bytes that can be retained in memory before using temporary files.

input
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://input`` is a read-only stream that provides access to the requested raw data. In the case of POST requests, it is better to use ``php://input`` instead of ``$HTTP_RAW_POST_DATA``, as it does not rely on specific php.ini directives. Also, in this case $HTTP_RAW_POST_DATA is not populated by default, potentially requiring less memory than if always_populate_raw_post_data is activated. When ``enctype="multipart/form-data"`` is used, ``php://input`` is invalid.

filter
----------------------------------------
``php://filter`` is a meta-wrapper designed for filtering applications when a data stream is opened. PHP provides some stream filters by default. In addition, various custom filters can also be used.

Filter has three parameters: resource, read, and write. The resource parameter is required. It specifies the data stream you want to filter. read and write are optional parameters that can set one or more filter names, separated by pipe characters (|).

filter list
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The list of registered filters can be obtained through ``stream_get_filters()``. The built-in filters in PHP are as follows:

- string filter
    - string.rot13
    - string.toupper
    - string.tolower
    - string.strip_tags
- Conversion filters
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

Filter exploit tricks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LFI
    - ``php://filter/convert.base64-encode/resource=index.php``
- When XXE reads a file, an error will be reported due to parsing, and base64 encoding can be used.
- base64 encoding will discard characters that are not in the code table and can be used to bypass some file formats
- Some converts consume a lot of resources and can be used as DoS
- rot13 / convert Convert through WAF
