other
=================================

low precision
---------------------------------
PHP does not use high precision to store floating point numbers, but uses the IEEE 754 double precision format, which may cause unexpected errors when comparing floating point numbers.
For example, ``php -r "var_dump(0.2+0.7==0.9);"`` The output of this line of code is ``bool(false)`` instead of ``bool(true)``. This may cause problems in some situations.

weak type
---------------------------------
If you use ``==`` to determine equality, some unexpected behavior will occur due to type inference, such as magic hash, which means that when two md5 values ​​​​are both ``0e[0-9]{30}``, the two hash values ​​will be considered equal.
In addition, when judging strings and numbers, PHP will automatically perform type conversion, so the result of ``1=="1a.php"`` will be true

In addition, when judging some hashes, if an array is passed in, the return value will be ``NULL``, so when judging the hash value of data from network requests, you need to first judge the data type.

Similarly, ``strcmp()`` ``ereg()`` ``strpos()`` these functions will also throw exceptions when processing arrays and return NULL.

command execution
---------------------------------
When the first parameter of preg_replace is //e, the second parameter will be executed as a command.

Truncate
---------------------------------
PHP characters have truncation behavior. You can use ``ereg`` / ``%00`` / ``iconv`` to implement PHP character truncation operations, thereby triggering the vulnerability.

variable override
---------------------------------
When using functions such as ``extract`` / ``parse_str``, or when using PHP's ``$$`` feature, if it is not called correctly, the user may be able to modify the variable arbitrarily.

php features
---------------------------------
- When php itself parses the request, if the parameter name contains the characters " ", ".", "[", it will convert them into underscores
- Due to historical reasons, ``urlencode`` is somewhat different from RFC3896. PHP also provides ``rawurlencode`` to implement the RFC3896 completion standard.

/tmp temporary file competition
---------------------------------
When phpinfo is accessible, the path to the uploaded temporary file can be seen, thus enabling LFI.
