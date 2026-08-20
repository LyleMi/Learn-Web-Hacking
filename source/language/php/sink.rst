Sink
=================================

arbitrary code execution
---------------------------------
- eval
- assert
- call_user_func

Execute system commands
---------------------------------
- pcntl_exec
- exec
- passthru
- popen
- shell_exec
- system
- proc_open

Magic function
---------------------------------
- ``__construct()`` is called when constructing an object
- ``__destruct()`` is called when the object is destroyed or the script ends
- ``__call()`` is called when calling a method that is inaccessible or does not exist
- ``__callStatic()`` is called when calling an inaccessible or non-existent static method
- ``__get()`` is called when reading an inaccessible or non-existent attribute
- ``__set()`` is called when assigning a value to an inaccessible or non-existent property
- ``__isset()`` is called when ``isset`` or ``empty()`` is called on an inaccessible or non-existent property
- ``__unset()`` is called when ``unset`` an inaccessible or non-existent property
- ``__sleep()`` is called when the object is serialized
- ``__wakeup()`` is called when the object is deserialized. If the value representing the number of object attributes in the serialized string is greater than the actual number of attributes, the execution of wakeup will be skipped.
- ``__toString()`` is called when a class is converted to a string
- ``__invoke()`` is called when the object is called as a function
- ``__set_state()`` is called when ``var_export()`` is exported
- ``__clone()`` is called when cloning an object
- ``__debugInfo()`` calls ``var_dump()`` which is called when printing an object

File related sensitive functions
---------------------------------
- ``move_uploaded_file``
- ``file_put_contents`` / ``file_get_contents``
- ``unlink``
- ``fopen`` / ``fgets``

SSRF
---------------------------------
- ``file_get_contents()``
- ``fsockopen()``
- ``curl_exec()``
- ``fopen()``
- ``readfile()``

phar trigger point
----------------------------------------
- fileatime / filectime / filemtime
- stat / fileinode / fileowner / filegroup / fileperms
- file / file_get_contents / readfile / fopen`
- file_exists / is_dir / is_executable / is_file / is_link / is_readable / is_writeable / is_writable
- parse_ini_file
- unlink
- copy
- exif
    - exif_thumbnail
    - exif_imagetype
- gd
    - imageloadfont
    - imagecreatefrom***
- hash
    - hash_hmac_file
    - hash_file
    - hash_update_file
    - md5_file
    - sha1_file
- file / url
    - get_meta_tags
    - get_headers
- standard
    - getimagesize
    - getimagesizefromstring

Native class utilization
---------------------------------
- XSS
    - Error
    - Exception
- SSRF
    - SoapClient
- open_basedir bypass
    - DirectoryIterator combined with ``glob://``
- XXE
    - SimpleXMLElement
