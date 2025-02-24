container
========================================

Common Java servers include Tomcat, Weblogic, JBoss, GlassFish, Jetty, Resin, IBM Websphere, etc. Here is a brief explanation of some frameworks.

Tomcat
----------------------------------------
Tomcat is a lightweight application server, which is widely used in small and medium-sized systems and concurrent access users, and is used to develop and debug JSP programs.

After receiving the request, Tomcat's processing flow is as follows:

- Client accesses the web server and sends HTTP requests
- After receiving the request, the web server passes it to the Servlet container
- Servlet container loads Servlet, generates Servlet instance, and passes objects representing request and response to it
- The Servlet instance uses the request object to obtain the client's request information, and then performs corresponding processing
- The Servlet instance sends the processing results back to the client through the response object. The container is responsible for ensuring that the response is sent correctly and returns control to the web server.

The Tomcat server is composed of a series of configurable components, where the core component is the Catalina Servlet container, which is the top-level container for all other Tomcat components.

Related CVE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2020-1938
- https://www.freebuf.com/vuls/228108.html
- CVE-2019-0232
- Remote code execution
- https://github.com/pyn3rd/CVE-2019-0232/
- CVE-2017-12615
- Any file writing
- https://mp.weixin.qq.com/s?__biz=MzI1NDg4MTIxMw==&mid=2247483659&idx=1&sn=c23b3a3b3b43d70999bdbe644e79f7e5
- CVE-2013-2067
- CVE-2012-4534
- CVE-2012-4431
- CVE-2012-3546
- CVE-2012-3544
- CVE-2012-2733
- CVE-2011-3375
- CVE-2011-3190
- CVE-2008-2938

Weblogic
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WebLogic is an Application Server produced by Oracle, the United States. It is a middleware based on the Java EE architecture. WebLogic is a Java application server used to develop, integrate, deploy and manage large distributed Web applications, network applications and database applications. It introduces the dynamic functions of Java and the security of Java Enterprise standards into the development, integration, deployment and management of large-scale network applications.

WebLogic provides comprehensive support for a variety of standards in the industry, including EJB, JSP, Servlet, JMS, JDBC, etc.

Related CVE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2019-2725
- wls-wsat deserialization remote code execution
- CVE-2019-2658
- CVE-2019-2650
- CVE-2019-2649
- CVE-2019-2648
- CVE-2019-2647
- CVE-2019-2646
- CVE-2019-2645
- CVE-2019-2618
- https://github.com/jas502n/cve-2019-2618/
- CVE-2019-2615
- CVE-2019-2568
- CVE-2018-3252
- CVE-2018-3248
- CVE-2018-3245
- CVE-2018-3201
- CVE-2018-3197
- CVE-2018-3191
- https://github.com/voidfyoo/CVE-2018-3191
- https://github.com/Libraggbond/CVE-2018-3191
- CVE-2018-2894
- Upload any file
- https://xz.aliyun.com/t/2458
- CVE-2018-2893
- Deserialization
- https://www.freebuf.com/vuls/178105.html
- CVE-2018-2628
- https://mp.weixin.qq.com/s/nYY4zg2m2xsqT0GXa9pMGA
- CVE-2018-1258
- CVE-2017-10271
- XMLDecoder deserialization vulnerability
- http://webcache.googleusercontent.com/search?q=cache%3AsH7j8TF8uOIJ%3Awww.freebuf.com%2Fvuls%2F160367.html
- CVE-2017-3248
- CVE-2016-3510
- CVE-2015-4852
- https://github.com/roo7break/serialator

JBoss
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
JBoss is a container and server that manages EJB based on J2EE, but the JBoss core service does not include WEB containers that support servlet/JSP, and is generally bound to Tomcat or Jetty.

Related CVE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2017-12149
- Deserialization vulnerability
- Visit ``/invoker/readonly``, if the page exists, there will be a deserialization vulnerability

Jetty
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Jetty is an open source servlet container.
