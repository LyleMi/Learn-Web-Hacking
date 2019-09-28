Phar
========================================

简介
----------------------------------------
Phar（PHP Archive）文件是一种打包格式，将PHP代码文件和其他资源放入一个文件中来实现应用程序和库的分发。

在来自Secarma的安全研究员Sam Thomas在18年的Black Hat上提出后利用方式后，开始受到广泛的关注。

Phar可利用是因为Phar以序列化的形式存储用户自定义的meta-data，而以流的形式打开的时候，会自动反序列化，从而触发对应的攻击载荷。

Phar文件结构
----------------------------------------
Phar由四个部分组成，分别是 ``stub`` / ``manifest`` / 文件内容 / 签名。 stub 需要 ``__HALT_COMPILER();`` 这个调用在PHP代码中。

manifest 包含压缩文件的权限、属性、序列化形式存储的meta-data等信息，这是攻击的核心部分，主要就是解析Phar时对meta-data的反序列化。

原理
----------------------------------------
phar的实现在 ``php-src/ext/phar/phar.c`` 中，主要是 ``phar_parse_metadata`` 函数在解析phar文件时调用了 ``php_var_unserialize`` ，因而造成问题。

而php在文件流处理过程中会调用 ``_php_stream_stat_path`` (/main/streams/streams.c) ，而后间接调用 ``phar_wrapper_stat`` ，所以大量的文件操作函数都可以触发phar的反序列问题。

目前已知部分的触发函数有:

fileatime / filectime / filemtime /stat / fileinode / fileowner / filegroup / fileperms / file / file_get_contents / readfile / fopen / file_exists / is_dir / is_executable / is_file / is_link / is_readable / is_writeable / is_writable / parse_ini_file / unlink / copy / exif_thumbnail / exif_imagetype / imageloadfont / imagecreatefrom*** / hash_hmac_file / hash_file / hash_update_file / md5_file / sha1_file / get_meta_tags / get_headers / getimagesize / getimagesizefromstring
