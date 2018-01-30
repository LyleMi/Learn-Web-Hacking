框架
================================

Django
--------------------------------

历史漏洞
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `CVE-2016-7401 CSRF Bypass <https://paper.seebug.org/58/>`_
- `CVE-2017-7233/7234 Open redirect vulnerability <https://www.djangoproject.com/weblog/2017/apr/04/security-releases/>`_
- `CVE-2017-12794 debug page XSS <https://www.leavesongs.com/PENETRATION/django-debug-page-xss.html>`_


配置相关
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Nginx 在为 Django 做反向代理时，静态文件目录配置错误会导致源码泄露。访问 /static.. 会 301 重定向到 /static../


Flask
--------------------------------
Flask默认使用客户端session，使得session可以被伪造