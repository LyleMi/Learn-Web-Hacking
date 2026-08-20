Phar
========================================

Introduction
----------------------------------------
Phar (PHP Archive) files are a packaging format that puts PHP code files and other resources into one file for distribution of applications and libraries.

After Sam Thomas, a security researcher from Secarma, proposed a post-exploitation method at Black Hat in 2018, it began to receive widespread attention.

Phar can be exploited because Phar stores user-defined meta-data in serialized form, and when opened in the form of a stream, it will be automatically deserialized, thus triggering the corresponding attack payload.

Phar file structure
----------------------------------------
Phar consists of four parts, namely ``stub`` / ``manifest`` / file content / signature. The stub requires ``__HALT_COMPILER();`` this call in PHP code.

The manifest contains the permissions, attributes of the compressed file, meta-data stored in serialized form and other information. This is the core part of the attack, mainly the deserialization of meta-data when parsing Phar.

principle
----------------------------------------
The implementation of phar is in ``php-src/ext/phar/phar.c``. The main problem is that the ``phar_parse_metadata`` function calls ``php_var_unserialize`` when parsing the phar file.

During the file stream processing process, PHP will call ``_php_stream_stat_path`` (/main/streams/streams.c), and then indirectly call ``phar_wrapper_stat``, so a large number of file operation functions can trigger the desequence problem of phar.

Some of the currently known trigger functions are:

fileatime / filectime / filemtime /stat / fileinode / fileowner / filegroup / fileperms / file / file_get_contents / readfile / fopen / file_exists / is_dir / is_executable / is_file / is_link / is_readable / is_writeable / is_writable / parse_ini_file / unlink / copy / exif_thumbnail / exif_imagetype / imageloadfont / imagecreatefrom*** / hash_hmac_file / hash_file / hash_update_file / md5_file / sha1_file / get_meta_tags / get_headers / getimagesize / getimagesizefromstring
