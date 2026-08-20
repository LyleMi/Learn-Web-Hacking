sandbox
================================

Commonly used functions
--------------------------------
- eval / exec / compile
- dir / type
- globals / locals / vars
- getattr / setattr

Import package method
--------------------------------
- ``import os``
- ``from os import *``
- ``__import__("os")``
- ``importlib``
- ``imp``
- ``reload(os)``
- ``execfile`` is only supported by Python2

bypass
--------------------------------
- ``dir(__builtins__)`` View built-in modules

- The simplest idea is to import in an existing module. If that module has already imported a module that can be used, it can be used.

- Find available modules in the parent class. The most common payload is ``().__class__.__bases__[0].__subclasses__()`` or use magic method to get the global scope ``__init__.__func__.__globals__``

- Some websites do not have filtering pickle modules. You can use pickle to implement arbitrary code execution. To generate payload, you can use ``https://gist.github.com/freddyb/3360650``

- Some sandboxes delete relevant module codes, so you can use functions in libc. In Python, you can generally use ctypes or cffi.

- ``"A""B" == "AB"``

defense
--------------------------------
Python officials give some defensive suggestions

- Use Jython and try to use the Java platform to lock down the program's permissions
- Use fakeroot to avoid
- Use some rootjail techniques
