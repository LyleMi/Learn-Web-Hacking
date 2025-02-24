Phar
========================================

Introduction
----------------------------------------
Phar (PHP Archive) file is a packaging format that places PHP code files and other resources into a file to implement the distribution of applications and libraries.

After the post-utilization method was proposed by the Secarma security researcher Sam Thomas in 2018, it began to attract widespread attention.

Phar can be used because Phar stores user-defined meta-data in serialized form, and when opened in stream form, it will automatically deserialize, triggering the corresponding attack payload.

Phar file structure
----------------------------------------
Phar consists of four parts: ``stub`` / ``manifest`` / file content / signature. stub requires ``__HALT_COMPILER();`` this call is in PHP code.

manifest contains information such as meta-data stored in the form of permissions, properties, serialization of compressed files. This is the core part of the attack, mainly deserialization of meta-data when parsing Phar.

principle
----------------------------------------
The implementation of php-src/ext/phar/phar.c` is mainly because the ``phar_parse_metadata`` function calls ``php_var_unserialize`` when parsing the phar file, thus causing problems.

During the file stream processing process, php will call ``_php_stream_stat_path`" (/main/streams/streams.c) and then indirectly call ``phar_wrapper_stat``, so a large number of file operation functions can trigger the desequence problem of phar.

Currently known parts of the trigger functions are:

fileatime / filectime / filemtime /stat / fileinode / fileowner / filegroup / fileperms / file / file_get_contents / readfile / fopen / file_exists / is_dir / is_executable / is_file / is_link / is_readable / is_writeable / is_writable / parse_ini_file / unlink / copy / exif_thumbnail / exif_imagetype / imageloadfont / imagecreatefrom*** / hash_hmac_file / hash_file / hash_update_file / md5_file / sha1_file / get_meta_tags / get_headers / getimagesize / getimagesizefromstring
