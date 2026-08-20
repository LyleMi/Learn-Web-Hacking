Classification
================================

Introduction
--------------------------------
The full name of XSS is Cross Site Scripting. In order to separate it from CSS, it is abbreviated as XSS. The Chinese name is cross-site scripting. This vulnerability occurs on the user side and refers to unexpected JavaScript code execution during the rendering process. XSS is usually used to obtain cookies, perform operations as the victim, etc.

Reflected XSS
--------------------------------
Reflected XSS is a relatively common and widespread category. For example, when the code of a website contains statements similar to the following: ``<?php echo "<p>hello, $_GET['user']</p>";?>`` , then set ``/?user=</p><script>alert("hack")</script><p>`` when accessing, and the preset JavaScript code can be executed.

Reflected XSS usually appears in functions such as search, and requires an attacker to click on the corresponding link to trigger it, and is greatly affected by defense methods such as XSS Auditor and NoScript.

Stored XSS
--------------------------------
Stored XSS is more harmful than reflective XSS. In this vulnerability, the attacker can store the attack payload in the server's database, causing a persistent attack.

DOM XSS
--------------------------------
The difference between DOM-type XSS is that DOM-type XSS is generally not directly related to the parsing response of the server, but is generated during the dynamic execution of JavaScript scripts.

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

Enter ``x' onerror='javascript:alert(/xss/)`` to trigger.

Blind XSS
--------------------------------
Blind XSS is a type of stored XSS that is stored in some storage, executed when a "victim" accesses the page, and renders the payload in the Document Object Model (DOM). The reason it's called Blind is because it usually happens with functionality that isn't normally exposed to the user.
