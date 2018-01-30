格式化字符串
================================

在Python中，有两种格式化字符串的方式，在Python2的较低版本中，格式化字符串的方式为 ``"this is a %s" % "test"`` ，之后增加了format的方式， 语法为 ``"this is a {}".format('test')`` 或者 ``"this is a {test}".format(test='test')``

当格式化字符串由用户输入时，则可能会造成一些问题，下面是一个最简单的例子

::

    >>> 'class of {0} is {0.__class__}'.format(42)
    "class of 42 is <class 'int'>"

从上面这个简单的例子不难知道，当我们可以控制要format的字符串时，则可以使用 ``__init__`` / ``__globals__`` 等属性读取一些比较敏感的值，甚至任意执行代码。