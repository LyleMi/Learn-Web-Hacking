WebDAV
========================================

Introduction
----------------------------------------
WebDAV (Web-based Distributed Authoring and Versioning) is a communication protocol based on HTTP 1.1 protocol. It extends HTTP 1.1 and adds some new methods in addition to several HTTP standard methods such as GET, POST, and HEAD, allowing applications to directly read and write to the Web Server, and supports write file locking, unlocking, and version control functions.

The supported methods are specifically:

- OPTIONS
- Get server support
- GET / PUT / POST / DELETE
- Resource operations
- TRACE
- Tracking server
- HEAD
- MKCOL
- Create collections
- PROPFIND / PROPPATCH
- COPY / MOVE
- LOCK / UNLOCK

Related CVEs
----------------------------------------
- CVE-2015-1833
    - Apache Jacrabbit WebDav XXE
    - http://www.securityfocus.com/archive/1/535582
- CVE-2015-7326
    - Milton WebDav XXE
    - http://www.securityfocus.com/archive/1/536813
