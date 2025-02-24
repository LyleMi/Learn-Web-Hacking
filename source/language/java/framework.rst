frame
========================================

Servlet
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Servlet (Server Applet) is the abbreviation of Java Servlet, called a mini-service program or service connector. It is a server-side program written in Java. Its main function is to interactively browse and modify data and generate dynamic Web content.

A Servlet in a narrow sense refers to an interface implemented by the Java language, and a Servlet in a broad sense refers to any class that implements this Servlet interface. Generally speaking, people understand Servlet as the latter. Servlets run on Java-enabled application servers. In principle, Servlets can respond to any type of request, but in most cases Servlets are only used to extend HTTP-based web servers.

Life cycle is
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The client requests the Servlet
- Loading Servlet class into memory
- Instantiate and call the init() method to initialize the Servlet
- service()(call ``doGet()``/``doPost()`` / ... / ``destroy()``````````

interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``init()``

During the lifetime of a servlet, the init() method is executed only once, which is executed when the server loads the servlet.

``service()``

The service() method is the core of the Servlet. Whenever a client requests an HttpServlet object, the ``service()`` method of the object is called and passed to this method a "ServletRequest" object and a "ServletResponse" object as parameters.

Struts 2
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Struts2 is a web application framework based on the MVC design pattern. It is essentially equivalent to a servlet. In the MVC design pattern, Struts2 serves as a controller to establish data interaction between the model and the view.

Request process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Tomcat server that the client sends requests
- Requested through a series of filters
- FilterDispatcher calls ActionMapper to determine whether this request wants to call an Action
- ActionMppaer decides to call an ActionFilterDispatcher to ActionProxy
- ActionProxy view structs.xml through Configuration Manager and find the corresponding Action class
- ActionProxy creates an ActionInvocation object
- ActionInvocation object callback Action execute method
- After the Action is executed, ActionInvocation finds the corresponding result based on the returned string and returns it to the server through HttpServletResponse

Related CVE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2016-3081 (S2-032)
- CVE-2016-3687 (S2-033)
- CVE-2016-4438 (S2-037)
- `CVE-2017-5638 <https://github.com/immunio/apache-struts2-CVE-2017-5638>`_
- CVE-2017-7672
- CVE-2017-9787
- CVE-2017-9793
- CVE-2017-9804
- `CVE-2017-9805 <https://github.com/mazen160/struts-pwn_CVE-2017-9805>`_
- `CVE-2017-12611 <https://github.com/brianwrf/S2-053-CVE-2017-12611>`_
- CVE-2017-15707
- CVE-2018-1327
- CVE-2018-11776

Spring
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring generally refers to Spring Framework, a lightweight Java application open source framework that provides a simple development method.

Spring MVC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring MVC is designed based on Spring's pattern. It is mainly used to develop web applications and simplify development.

Spring Boot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring's solution was quite cumbersome at the beginning of its launch, so it provided Spring Boot as an automated configuration tool to reduce the complexity of project construction.

Request process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- User sends requests to the server
- The server receives a request and uses DispatchServlet to handle it
- Dispatch uses HandleMapping to check whether the url has a corresponding controller. If so, execute
- If Controller returns a string, ViewResolver converts the string into the corresponding view object
- DispatchServlet outputs the data in the view object to the server
- The server outputs data to the client

CVE Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2018-1270
- Spring Websocket Remote Code Execution Vulnerability
- Spring Framework 5.0 - 5.0.5
- Spring Framework 4.3 - 4.3.15
- CVE-2018-1273
- Spring Data Remote Code Execution Vulnerability
- Spring Data Commons 1.13 - 1.13.10
- Spring Data Commons 2.0 - 2.0.5
- Spring Data REST 2.6 - 2.6.10
- Spring Data REST 3.0 - 3.0.5
- CVE-2017-8046
- Spring Data REST Remote Code Execution Vulnerability
- CVE-2017-4971
- Spring Web Flow Remote Code Execution Vulnerability

Shiro
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro is a powerful and easy to use Java security framework that includes authentication, authorization, encryption, and session management.

CVE Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2020-13933
- Apache Shiro < 1.6.0
- Authentication bypass vulnerability
- CVE-2020-11989
- SHIRO-782
- Apache Shiro < 1.5.3
- Authentication bypass vulnerability
- CVE-2020-1957
- SHIRO-682
- Apache Shiro < 1.5.2
- Authentication bypass vulnerability
- CVE-2019-12422
- SHIRO-721
- Apache Shiro < 1.4.2
- Padding Oracle Attack Remote Code Execution Vulnerability
- CVE-2016-4437
- SHIRO-550
- Apache Shiro <= 1.2.4
- Deserialization remote code execution vulnerability
- CVE-2014-0074
- SHIRO-460
- Apache Shiro < 1.2.3
- Authentication bypass vulnerability

CVE-2020-13933
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before Apache Shiro 1.6.0, since the matching process of Shiro interceptor and requestURI is different from that of the web framework's interceptor, the attacker constructs a special http request, which can bypass Shiro's authentication and is sensitive to unauthorized access. path.

CVE-2020-11989
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before Apache Shiro 1.5.3, since the matching process of Shiro interceptor and requestURI is different from that of the web framework's interceptor, the attacker constructs a special http request, which can bypass Shiro's authentication and is sensitive to unauthorized access. path. There are two ways to attack this vulnerability.

CVE-2020-1957
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before Apache Shiro 1.5.2, since the matching process of Shiro interceptor and requestURI is different from that of the web framework's interceptor, the attacker constructs a special http request, which can bypass Shiro's authentication and is sensitive to unauthorized access. path.

CVE-2019-12422
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The versions before Apache Shiro use the ``AES/CBC/PKCS5Padding`` mode encryption by default. The Shiro component with RememberMe enabled will allow remote attackers to construct serialized data and blast through Padding Oracle Attack, even if the secret key is unknown. Under the conditions of , any command can also be executed on the target server.

CVE-2016-4437
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro versions before 1.2.5 have the default AES key ``kPH+bIxk5D2deZiIxcaaaA==`` in the ``org.apache.shiro.mgt.AbstractRememberMeManager``. Shiro component that enables RememberMe function will allow remote attackers to construct. Serialize data and execute any command on the target server.
