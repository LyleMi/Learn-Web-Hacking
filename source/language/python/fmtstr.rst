Format string
================================

In Python, there are two ways to format strings. In lower versions of Python 2, the way to format strings is ``"this is a %s" % "test"``. Later, the format method was added. The syntax is ``"this is a {}".format('test')`` or ``"this is a {test}".format(test='test')``

When the format string is entered by the user, it may cause some problems. The following is the simplest example.

::

    >>> 'class of {0} is {0.__class__}'.format(42)
    "class of 42 is <class 'int'>"

It is not difficult to know from the above simple example that when we can control the string to be formatted, we can use attributes such as ``__init__`` / ``__globals__`` to read some more sensitive values, or even execute code arbitrarily.