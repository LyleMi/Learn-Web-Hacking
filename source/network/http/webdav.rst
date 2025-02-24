WebDav
========================================

Introduction
----------------------------------------
WebDAV (Web-based Distributed Authoring and Versioning) A communication protocol based on the HTTP 1.1 protocol. It extends HTTP 1.1 and adds some new methods in addition to several HTTP standard methods such as GET, POST, HEAD, etc., so that applications can read and write directly to Web Server, and supports functions such as file locking, unlocking, and version control. .

The supported methods are:

- OPTIONS
- Get server support
- GET / PUT / POST / DELETE
- Resource Operation
- TRACE
- Tracking server
- HEAD
- MKCOL
- Create a collection
- PROPFIND / PROPPATCH
- COPY / MOVE
- LOCK / UNLOCK

Related CVE
----------------------------------------
- CVE-2015-1833
- Apache Jacrabbit WebDav XXE
- http://www.securityfocus.com/archive/1/535582
- CVE-2015-7326
- Milton Webdav XXE
- http://www.securityfocus.com/archive/1/536813
