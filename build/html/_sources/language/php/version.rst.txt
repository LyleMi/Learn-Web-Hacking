Version security changes
========================================

8.0
----------------------------------------
- Comparison of string vs. number weak type will first convert the number to string and then compare two strings
-Exception throws instead of warning when introspecting errors in internal parameters
- ``assert`` no longer supports code execution
- Remove ``create_function``
- Remove the e-mode in ``mb_ereg_replace()``
- Meta-information in Phar is no longer automatically deserialized
-`parse_str`` must be passed in the second parameter
- Remove ``string.strip_tags`` in ``php://filter``

7.2
----------------------------------------
- String without quotes will produce E_WARNING
- create_function abandoned
- assert cannot pass in string expressions
- Using parse_str() without the second parameter will generate an E_DEPRECATED warning
- __autoload() is abandoned

7.1
----------------------------------------
- Insufficient parameters provided by calling user-defined functions will throw an error exception instead of a warning
- No more destructors are called on incomplete objects
- call_user_func() no longer supports calls to addressed functions
- The e-pattern modifiers for mb_ereg_replace() and mb_ereg_replace() are discarded
- ext/mcrypt is abandoned

7.0
----------------------------------------
- preg_replace " " modifier generates an E_WARNING error and is invalid
- Remove all ext/mysql functions
- Remove all ext/mssql functions
- Remove call_user_method() and call_user_method_array()
- foreach no longer changes internal array pointers
- Previously, if an octal character contains an invalid number, the invalid number will be silently abridged (0128 will be parsed as 012), and now such an octal character will produce a parsing error
- Hexadecimal strings are no longer considered as numbers
- dl() is no longer available in PHP-FPM, and is still available in CLI and embedded SAPIs
- Remove ASP and script PHP tags, i.e. ``<% %>`` / ``<%= %>`` / ``<script language="php"> </script>``
- When the value overflows, the internal function will fail
- $HTTP_RAW_POST_DATA was removed

5.6
----------------------------------------
- $HTTP_RAW_POST_DATA is abandoned
- CURLOPT_SAFE_UPLOAD must be set to FALSE before you can use the @file syntax to upload files

5.5
----------------------------------------
- preg_replace " " modifier generates E_DEPRECATED error
- Abandoned ``mysql_*` series functions

5.4
----------------------------------------
- Safe mode is no longer supported
- Remove Magic Quotes
- Converting an array into a string will produce an E_NOTICE level error
