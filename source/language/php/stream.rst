PHP流
========================================

简介
----------------------------------------
流（Streams）的概念是在php 4.3引入的，是对流式数据的抽象，用于统一数据操作，比如文件数据、网络数据、压缩数据等。

流可以通过file、open、fwrite、fclose、file_get_contents、
file_put_contents等函数操作。

封装协议
----------------------------------------
PHP 带有很多内置 URL 风格的封装协议，可用于类似 fopen()、 copy()、 file_exists() 和 filesize() 的文件系统函数。支持的协议可用 ``stream_get_wrappers()`` 查看。

- ``file://`` 访问本地文件系统
- ``http://`` 访问 HTTP(s) 网址
- ``ftp://`` 访问 FTP(s) URLs
- ``php://`` 访问各个输入/输出流（I/O streams）
- ``zlib://`` 压缩流
- ``data://`` 数据（RFC 2397）
- ``glob://`` 查找匹配的文件路径模式
- ``phar://`` PHP 归档
- ``ssh2://`` Secure Shell 2
- ``rar://`` RAR
- ``ogg://`` 音频流
- ``expect://`` 处理交互式的流

PHP支持流
----------------------------------------
PHP 提供了一些输入/输出（IO）流，允许访问 PHP 的输入输出流、标准输入输出和错误描述符，内存中、磁盘备份的临时文件流以及可以操作其他读取写入文件资源的过滤器。 

需要注意的是，流不受 ``allow_url_fopen`` 限制，但是 ``php://input``、 ``php://stdin``、 ``php://memory`` 和 ``php://temp`` 受限于 ``allow_url_include`` 。

输入输出流
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://stdin`` 、 ``php://stdout`` 和 ``php://stderr`` 允许直接访问 PHP 进程相应的输入或者输出流。数据流引用了复制的文件描述符，所以如果在打开 ``php://stdin`` 并在之后关了它，仅是关闭了复制品，真正被引用的 STDIN 并不受影响。

其中 ``php://stdin`` 是只读的， ``php://stdout`` 和 ``php://stderr`` 是只写的。 

fd
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
php://fd 允许直接访问指定的文件描述符。例如 ``php://fd/3`` 引用了文件描述符 3。 

memory与temp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://memory`` 和 ``php://temp`` 是一个类似文件包装器的数据流，允许读写临时数据。两者的唯一区别是 ``php://memory`` 总是把数据储存在内存中，而 ``php://temp`` 会在内存量达到预定义的限制后（默认是 2MB）存入临时文件中。临时文件位置的决定和 ``sys_get_temp_dir()`` 的方式一致。

``php://temp`` 的内存限制可通过添加 ``/maxmemory:NN`` 来控制，NN 是以字节为单位、保留在内存的最大数据量，超过则使用临时文件。 

input
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``php://input`` 是个可以访问请求的原始数据的只读流。 POST 请求的情况下，最好使用 ``php://input`` 来代替 ``$HTTP_RAW_POST_DATA``，因为它不依赖于特定的 php.ini 指令。而且，这样的情况下 ``$HTTP_RAW_POST_DATA`` 默认没有填充，比激活 ``always_populate_raw_post_data`` 潜在需要更少的内存。 ``enctype="multipart/form-data"`` 的时候 ``php://input`` 是无效的。 

filter
----------------------------------------
``php://filter`` 是一种元封装器，设计用于数据流打开时的筛选过滤应用。PHP默认提供了一些流过滤器，除此之外，还可以使用各种自定义过滤器。

filter有resource, read, write三个参数，resource参数是必须的。它指定了你要筛选过滤的数据流。 read和write是可选参数，可以设定一个或多个过滤器名称，以管道符（|）分隔。

过滤器列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
可以通过 ``stream_get_filters()`` 获取已经注册的过滤器列表。其中PHP内置的过滤器如下：

- 字符串过滤器
    - string.rot13
    - string.toupper
    - string.tolower
    - string.strip_tags
- 转换过滤器
    - convert.base64-encode
    - convert.base64-decode
    - convert.quoted-printable-encode
    - convert.quoted-printable-decode
    - convert.iconv.*
- 压缩过滤器
    - zlib.deflate
    - zlib.inflate
    - bzip2.compress
    - bzip2.decompress
- 加密过滤器
    - mcrypt.``ciphername``
    - mdecrypt.``ciphername``

过滤器利用tricks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- LFI
    - ``php://filter/convert.base64-encode/resource=index.php``
- XXE读取文件时会因而解析报错，可用base64编码
- base64编码会弃掉未在码表内的字符，可用于绕过一些文件格式
- 部分 convert 会有大量的资源消耗，可用作DoS
- rot13 / convert 转换 过WAF
