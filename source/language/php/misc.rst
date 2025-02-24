other
=================================

Low precision
---------------------------------
In PHP, it is not to use high precision to store floating point numbers, but to use IEEE 754 double precision format, which may cause unexpected errors when comparing floating point numbers.
For example, ``php -r "var_dump(0.2+0.7==0.9);"``` The output of this line of code is ``bool(false)`` instead of ``bool(true)`. This can be problematic in some cases.

Weak type
---------------------------------
If you use ``==`` to determine equality, some unexpected behavior will occur due to type inference, such as magic hash, which means that when both md5 values are ``0e[0-9]{30}`` When , the two hash values are considered equal.
In addition, when judging strings and numbers, PHP will automatically convert type, so the result of ``1=="1a.php"`` will be true

In addition, when judging some hashs, if the incoming array is an array, the return value will be ``NULL``. Therefore, when judging the hash value of data requested from the network, you need to first determine the data type.

Similarly, these functions will also be exceptions when processing arrays, returning NULL.

Command execution
---------------------------------
When the first parameter is //e, the second parameter will be executed as a command

Cutoff
---------------------------------
PHP characters have truncation behavior, and you can use ``ereg``/`%00``/``iconv`` and other operations to implement php character truncation, thereby triggering vulnerabilities.

Variable overlay
---------------------------------
When using functions such as ``extract`` / ``parse_str``, or using php's ``$$`` feature, if there is no correct call, it may allow the user to modify the variable at will.

PHP Features
---------------------------------
- When php itself parses the request, if the parameter name contains the characters "", "." and "[", they will be converted into underscores
- Due to historical reasons, there are certain differences between ``urlencode`` and RFC3896. PHP also provides the implementation of the RFC3896 completion standard

/tmp temporary file competition
---------------------------------
When phpinfo is accessible, you can see the path of the uploaded temporary file, thereby realizing LFI.
