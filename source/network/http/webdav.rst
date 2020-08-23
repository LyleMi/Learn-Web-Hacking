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
