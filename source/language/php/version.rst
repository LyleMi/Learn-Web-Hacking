Version security changes
========================================

8.0
----------------------------------------
- Weakly typed comparison of strings and numbers will first convert the number to a string, and then compare the two strings
- Throw an exception instead of a warning when internal parameter introspection fails
- ``assert`` no longer supports executing code
- Removed ``create_function``
- Remove e mode in ``mb_ereg_replace()``
- Meta information in Phar is no longer automatically deserialized
- ``parse_str`` must be passed in the second parameter
- Removed ``string.strip_tags`` in ``php://filter``

7.2
----------------------------------------
- Unquoted strings will generate E_WARNING
- create_function is deprecated
- assert cannot pass in a string expression
- Using parse_str() without a second argument produces an E_DEPRECATED warning
- __autoload() is deprecated

7.1
----------------------------------------
- Calling a user-defined function with insufficient arguments will throw an error exception instead of a warning
- Destructor methods are no longer called on incomplete objects
- call_user_func() no longer supports calling functions passed by address
- The e-mode modifier of mb_ereg_replace() and mb_eregi_replace() is deprecated
- ext/mcrypt is deprecated

7.0
----------------------------------------
- preg_replace "\e" modifier generates E_WARNING error and is invalid
- Remove all ext/mysql functions
- Remove all ext/mssql functions
- Removed call_user_method() and call_user_method_array()
- foreach no longer changes the internal array pointer
- Previously, if an octal character contained invalid digits, the invalid digits would be silently truncated (0128 would be parsed as 012). Now such octal characters will generate a parsing error.
- Hexadecimal strings are no longer considered numbers
- dl() is no longer available in PHP-FPM, still available in CLI and embed SAPIs
- Removed ASP and script PHP tags, i.e. ``<% %>`` / ``<%= %>`` / ``<script language="php"> </script>``
- In case of numerical overflow, the internal function will fail
- $HTTP_RAW_POST_DATA removed

5.6
----------------------------------------
- $HTTP_RAW_POST_DATA is deprecated
- CURLOPT_SAFE_UPLOAD must be set to FALSE before you can use the @file syntax to upload files

5.5
----------------------------------------
- preg_replace "\e" modifier produces E_DEPRECATED error
- Abandoned ``mysql_*`` series of functions

5.4
----------------------------------------
- Safe mode is no longer supported
- Remove magic quotes
- Converting an array to a string will generate an E_NOTICE level error
