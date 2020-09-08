分类
================================

简介
--------------------------------
XSS全称为Cross Site Scripting，为了和CSS分开简写为XSS，中文名为跨站脚本。该漏洞发生在用户端，是指在渲染过程中发生了不在预期过程中的JavaScript代码执行。XSS通常被用于获取Cookie、以受攻击者的身份进行操作等行为。

反射型XSS
--------------------------------
反射型XSS是比较常见和广泛的一类，举例来说，当一个网站的代码中包含类似下面的语句：``<?php echo "<p>hello, $_GET['user']</p>";?>`` ，那么在访问时设置 ``/?user=</p><script>alert("hack")</script><p>`` ，则可执行预设好的JavaScript代码。

反射型XSS通常出现在搜索等功能中，需要被攻击者点击对应的链接才能触发，且受到XSS Auditor、NoScript等防御手段的影响较大。

储存型XSS
--------------------------------
储存型XSS相比反射型来说危害较大，在这种漏洞中，攻击者能够把攻击载荷存入服务器的数据库中，造成持久化的攻击。

DOM XSS
--------------------------------
DOM型XSS不同之处在于DOM型XSS一般和服务器的解析响应没有直接关系，而是在JavaScript脚本动态执行的过程中产生的。

例如

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

输入 ``x' onerror='javascript:alert(/xss/)`` 即可触发。

Blind XSS
--------------------------------
Blind XSS是储存型XSS的一种，它保存在某些存储中，当一个“受害者”访问这个页面时执行，并且在文档对象模型(DOM)中呈现payload。 它被称为Blind的原因是因为它通常发生在通常不暴露给用户的功能上。
