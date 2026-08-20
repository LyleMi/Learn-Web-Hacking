frame
================================

Django
--------------------------------

Historical holes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `CVE-2016-7401 CSRF Bypass <https://paper.seebug.org/58/>`_
- `CVE-2017-7233/7234 Open redirect vulnerability <https://www.djangoproject.com/weblog/2017/apr/04/security-releases/>`_
- `CVE-2017-12794 debug page XSS <https://www.leavesongs.com/PENETRATION/django-debug-page-xss.html>`_


Configuration related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- When Nginx is used as a reverse proxy for Django, incorrect static file directory configuration may lead to source code leakage. Accessing /static.. will 301 redirect to /static../


Flask
--------------------------------
Flask uses client sessions by default, allowing sessions to be forged.