Classification
================================

Introduction
--------------------------------
XSS is full name Cross Site Scripting. In order to be abbreviated as XSS from CSS, it is called Cross-site scripting in Chinese. This vulnerability occurs on the user side, which refers to the JavaScript code execution that occurs during the rendering process that is not in the expected process. XSS is usually used to obtain cookies, operate as an attacker, and other behaviors.

Reflective XSS
--------------------------------
Reflective XSS is a relatively common and widespread category. For example, when a website's code contains a statement similar to the following: ``<?php echo "<p>hello, $_GET['user']</p >";?>`` , then when accessing ``/?user=</p><script>alert("hack")</script><p>`` , you can execute preset JavaScript Code.

Reflective XSS usually appears in search and other functions. It needs to be triggered by the attacker clicking the corresponding link, and is greatly affected by defense methods such as XSS Auditor and NoScript.

Storage XSS
--------------------------------
Storage XSS is more harmful than reflective. In this vulnerability, an attacker can store the attack payload into the server's database, causing a persistent attack.

DOM XSS
--------------------------------
The difference between DOM-type XSS is that DOM-type XSS generally has no direct relationship with the server's parsing response, but is generated during the dynamic execution of JavaScript scripts.

For example

::

<html>
<head>
<title>DOM Based XSS Demo</title>
<script>
function xsstest()
{
var str = document.getElementById("input").value;
document.getElementById("output").innerHTML = "<img src='"+str+"'></img>";
}
</script>
</head>
<body>
<div id="output"></div>
<input type="text" id="input" size=50 value="" />
<input type="button" value="submit" onclick="xsstest()" />
</body>
</html>

Enter ``x' oneerror='javascript:alert(/xss/)`` to trigger.

Blind XSS
--------------------------------
Blind XSS is a type of storage XSS that is stored in some storage, executed when a "victim" accesses this page, and presents a payload in the Document Object Model (DOM). The reason it is called Blind is because it usually occurs on features that are not usually exposed to the user.
