Format string
================================

In Python, there are two ways to format strings. In the lower version of Python2, the way to format strings is ``"this is a %s" % "test"``, and then format The syntax is ``"this is a {}".format('test')`` or ``"this is a {test}".format(test='test')``

Some problems can be caused when formatting strings are entered by the user. Here is a simplest example

::

>>> 'class of {0} is {0.__class__}'.format(42)
"class of 42 is <class 'int'>"

From the simple example above, it is not difficult to know that when we can control the string to format, we can use properties such as ``__init__` / ``__globals__`` to read some more sensitive values, and even execute code arbitrarily.
