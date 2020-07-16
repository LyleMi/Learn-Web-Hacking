沙箱
================================

常用函数
--------------------------------
- eval / exec / compile
- dir / type
- globals / locals / vars
- getattr / setattr

导入包方式
--------------------------------
- ``import os``
- ``from os import *``
- ``__import__("os")``
- ``importlib``
- ``imp``
- ``reload(os)``
- ``execfile`` 仅Python2支持

绕过
--------------------------------
- ``dir(__builtins__)`` 查看内置模块

- 最简单的思路是在已有的模块中import，如果那个模块中已经 import 可以利用的模块就可以使用了

- 在父类中寻找可用的模块，最常见payload是 ``().__class__.__bases__[0].__subclasses__()`` 或者用魔术方法获取全局作用域 ``__init__.__func__.__globals__``

- 有些网站没有过滤 pickle 模块，可以使用 pickle 实现任意代码执行，生成 payload 可以使用 ``https://gist.github.com/freddyb/3360650``

- 有的沙箱把相关的模块代码都被删除了，则可以使用libc中的函数，Python 中调用一般可以使用 ctypes 或者 cffi。

- ``"A""B" == "AB"``

防御
--------------------------------
Python官方给出了一些防御的建议

- 使用Jython并尝试使用Java平台来锁定程序的权限
- 使用fakeroot来避免
- 使用一些rootjail的技术
