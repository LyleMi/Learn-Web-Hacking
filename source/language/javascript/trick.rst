Trick
========================================

通过正则表达式构造特定字符
----------------------------------------
.. code-block:: javascript

    empty = RegExp.prototype.flags
    regSource = { ...RegExp.prototype.source }
    regSource.toString = Array.prototype.shift
    regSource.length = 4
    left  = regSource + empty // 生成 (
    quest = regSource + empty // 生成 ?
    colon = regSource + empty // 生成 :
    right = regSource + empty // 生成 )

    xss = {}
    xss.source = 'xss'
    xss.flags = 'a'
    xss.toString = RegExp.prototype.toString
    xss + "" // => /xss/a
