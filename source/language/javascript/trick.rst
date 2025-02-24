Trick
========================================

Constructing specific characters through regular expressions
----------------------------------------
.. code-block:: javascript

empty = RegExp.prototype.flags
regSource = { ...RegExp.prototype.source }
regSource.toString = Array.prototype.shift
regSource.length = 4
left = regSource + empty // Generate (
quest = regSource + empty // Generate ?
colon = regSource + empty // Generate:
right = regSource + empty // generated)

xss = {}
xss.source = 'xss'
xss.flags = 'a'
xss.toString = RegExp.prototype.toString
xss + "" // => /xss/a
