frame
================================

Django
--------------------------------

Historical loopholes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `CVE-2016-7401 CSRF Bypass <https://paper.seebug.org/58/>`_
- `CVE-2017-7233/7234 Open redirect vulnerability <https://www.djangoproject.com/weblog/2017/apr/04/security-releases/>`_
- `CVE-2017-12794 debug page XSS <https://www.leavesongs.com/PENETRATION/django-debug-page-xss.html>`_


Configuration related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Nginx When doing a reverse proxy for Django, static file directory configuration errors can lead to source code leakage. Access to /static.. will redirect 301 to /static../


Flask
--------------------------------
Flask uses client session by default, so that session can be forged
