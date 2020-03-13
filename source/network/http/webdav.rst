WebDAV
========================================

简介
----------------------------------------
WebDAV （Web-based Distributed Authoring and Versioning） 一种基于 HTTP 1.1协议的通信协议。它扩展了HTTP 1.1，在GET、POST、HEAD等几个HTTP标准方法以外添加了一些新的方法，使应用程序可对Web Server直接读写，并支持写文件锁定、解锁，以及版本控制等功能。

支持的方法具体为：

- OPTIONS
    - 获取服务器的支持
- GET / PUT / POST / DELETE
    - 资源操作
- TRACE
    - 跟踪服务器
- HEAD
- MKCOL
    - 创建集合
- PROPFIND / PROPPATCH
- COPY / MOVE
- LOCK / UNLOCK

相关CVE
----------------------------------------
- CVE-2015-1833
    - Apache Jacrabbit WebDav XXE
    - http://www.securityfocus.com/archive/1/535582
- CVE-2015-7326
    - Milton WebDav XXE
    - http://www.securityfocus.com/archive/1/536813

参考链接
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 3253 <https://tools.ietf.org/html/rfc3253>`_ Versioning Extensions to WebDAV (Web Distributed Authoring and Versioning)
- `RFC 3648 <https://tools.ietf.org/html/rfc3648>`_ Web Distributed Authoring and Versioning (WebDAV) Ordered Collections Protocol
- `RFC 3744 <https://tools.ietf.org/html/rfc3744>`_ Web Distributed Authoring and Versioning (WebDAV) Access Control Protocol
- `RFC 4437 <https://tools.ietf.org/html/rfc4437>`_ Web Distributed Authoring and Versioning (WebDAV) Redirect Reference Resources
- `RFC 4918 <https://tools.ietf.org/html/rfc4918>`_ HTTP Extensions for Web Distributed Authoring and Versioning (WebDAV)
- `RFC 5323 <https://tools.ietf.org/html/rfc5323>`_ Web Distributed Authoring and Versioning (WebDAV) SEARCH
- `RFC 5842 <https://tools.ietf.org/html/rfc5842>`_ Binding Extensions to Web Distributed Authoring and Versioning (WebDAV)

Blog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `What should a hacker know about WebDav <http://2015.zeronights.org/assets/files/35-Egorov.pdf>`_
