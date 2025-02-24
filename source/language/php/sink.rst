Sink
=================================

Execute any code
---------------------------------
- eval
- assert
- call_user_func

Execute system commands
---------------------------------
- pcntl_exec
- exec
- passthru
- Popping
- shell_exec
- system
- proc_open

Magic functions
---------------------------------
- ``__construct()`` is called when building an object
- ``__destruct()`` is called when the object or script is destroyed
- ``__call()`` is called when calling an inaccessible or non-existent method
- ``__callStatic()`` is called when calling an inaccessible or non-existent static method
- ``__get()`` is called when reading an inaccessible or non-existent property
- ``__set()`` is called when assigning values to inaccessible or non-existent properties
- ``__isset()` is called when calling ``isset`` or ``empty()`` property that is not accessible or non-existent
- ``__unset()`` is called when an unreachable or non-existent property is performed
- ``__sleep()`` is called when serializing the object
- ``__wakeup()`` is called when deserializing the object. The value of the serialization string representing the number of objects attributes is greater than the real number of properties, the execution of wakeup will be skipped.
- ``__toString()`` is called when a class is converted to a string
- ``__invoke()`` object is called when it is called function-like
- ``__set_state()`` Called ``var_export()``
- ``__clone()`` is called when performing object clone
- ``__debugInfo()`` Called ``var_dump()`` when printing the object

File-related sensitive functions
---------------------------------
- ``move_uploaded_file``
- ``file_put_contents`` / ``file_get_contents``
- ``unlink``
- ``fopen`` / ``fgets``

SSRF
---------------------------------
- ``file_get_contents()``
- `` fsock opening () ``
- ``curl_exec()``
- `` Fopen () `` ``
- ``readfile()``

phar trigger point
----------------------------------------
- fileatime / filectime / filemtime
- stat / fileinode / fileowner / filegroup / fileperms
- file / file_get_contents / readfile / fopen`
- file_exists / is_dir / is_executable / is_file / is_link / is_readable / is_writeable / is_writable
- Parse_ini_file
- unlink
- copy
- exif
- exif_thumbnail
- Exif_imagetype
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
