Sandbox
================================

Common functions
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
- `` reload (OS) ``
- ``execfile`` Python2 only supports

Bypass
--------------------------------
- ``dir(__builtins__)`` View built-in modules

- The simplest idea is to import in an existing module. If the module already imports the module that can be used, it can be used.

- Looking for available modules in the parent class, the most common payload is ``().__class__.__bases__[0].__subclasses__()`` or use magic methods to get the global scope ``__init__.__func__.__globals__```

- Some websites do not have a filter pickle module. You can use pickle to implement arbitrary code execution. To generate payload, you can use ``https://gist.github.com/freddyb/3360650``

- Some sandboxes have deleted the relevant module code, so you can use functions in libc. Calls in Python can generally use ctypes or cffi.

- ``"A""B" == "AB"``

defense
--------------------------------
Python official gives some defense suggestions

- Use Jython and try to use the Java platform to lock the permissions of the program
- Use fakeroot to avoid
- Using some rootjail techniques
