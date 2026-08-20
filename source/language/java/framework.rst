frame
========================================

Servlet
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Servlet (Server Applet) is the abbreviation of Java Servlet, called a small service program or service connector. It is a server-side program written in Java. Its main function is to browse and modify data interactively and generate dynamic Web content.

Servlet in the narrow sense refers to an interface implemented by the Java language, and Servlet in the broad sense refers to any class that implements this Servlet interface. Generally, people understand Servlet as the latter. Servlets run in Java-enabled application servers. In principle, Servlets can respond to any type of request, but in most cases Servlets are only used to extend Web servers based on the HTTP protocol.

The life cycle is
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The client requests the Servlet
- Load Servlet class into memory
- Instantiate and call the init() method to initialize the Servlet
- service()(called ``doGet()`` / ``doPost()`` / ... / ``destroy()`` depending on the request method

interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``init()`` 

During the life of the Servlet, the init() method is executed only once, when the server loads the Servlet.

``service()``

The service() method is the core of Servlet. Whenever a client requests an HttpServlet object, the object's service() method is called, and a "Request" (ServletRequest) object and a "Response" (ServletResponse) object are passed to this method as parameters.

Struts 2
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Struts2 is a Web application framework based on the MVC design pattern. It is essentially equivalent to a servlet. In the MVC design pattern, Struts2 acts as a controller to establish data interaction between the model and the view.

Request process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The client sends the request to the tomcat server
- The request goes through a series of filters
- FilterDispatcher calls ActionMapper to determine whether this request should call an Action
- ActionMppaer decides to call an ActionFilterDispatcher to send the request to ActionProxy
- ActionProxy checks structs.xml through Configuration Manager and finds the corresponding Action class
- ActionProxy creates an ActionInvocation object
- ActionInvocation object callback Action's execute method
- After the Action is executed, ActionInvocation finds the corresponding result based on the returned string and returns it to the server through HttpServletResponse.

Related CVEs
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
Spring generally refers to Spring Framework, a lightweight Java application open source framework that provides an easy development method.

Spring MVC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring MVC is an MVC framework designed based on Spring's pattern. It is mainly used to develop Web applications and simplify development.

Spring Boot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When Spring was launched, the solution was relatively cumbersome, so Spring Boot was provided as an automated configuration tool to reduce the complexity of project construction.

Request process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The user sends a request to the server
- The server receives the request and uses DispatchServlet to process it
- Dispatch uses HandleMapping to check whether the url has a corresponding Controller. If so, execute it.
- If the Controller returns a string, ViewResolver converts the string into the corresponding view object
- DispatchServlet outputs the data in the view object to the server
- The server outputs data to the client

CVE overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2018-1270
    - Spring Websocket remote code execution vulnerability
    - Spring Framework 5.0 - 5.0.5
    - Spring Framework 4.3 - 4.3.15
- CVE-2018-1273
    - Spring Data remote code execution vulnerability
    - Spring Data Commons 1.13 - 1.13.10
    - Spring Data Commons 2.0 - 2.0.5
    - Spring Data REST 2.6 - 2.6.10
    - Spring Data REST 3.0 - 3.0.5
- CVE-2017-8046
    - Spring Data REST remote code execution vulnerability
- CVE-2017-4971
    - Spring Web Flow remote code execution vulnerability

Shiro
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro is a powerful and easy-to-use Java security framework with features including authentication, authorization, encryption, and session management.

CVE overview
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
    - Padding Oracle Attack remote code execution vulnerability
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
In versions before Apache Shiro 1.6.0, because the matching process between Shiro interceptor and requestURI is different from that of the web framework's interceptor, an attacker can construct a special http request that can bypass Shiro's authentication and access sensitive paths without authorization.

CVE-2020-11989
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before Apache Shiro 1.5.3, due to the difference between the matching process between Shiro interceptor and requestURI and the matching process of web framework's interceptor, an attacker can construct a special http request to bypass Shiro's authentication and gain unauthorized access to sensitive paths. There are two attack methods for this vulnerability.

CVE-2020-1957
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions prior to Apache Shiro 1.5.2, due to the difference between the matching process between the Shiro interceptor and the requestURI and the matching process of the web framework's interceptor, an attacker can construct a special http request that can bypass Shiro's authentication and access sensitive paths without authorization.

CVE-2019-12422
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Versions before Apache Shiro 1.4.2 use ``AES/CBC/PKCS5Padding`` mode encryption by default. The Shiro component with the RememberMe function enabled will allow remote attackers to construct serialized data and blast it through Padding Oracle Attack. Even if the secret key is unknown, arbitrary commands can be executed on the target server.

CVE-2016-4437
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Versions before Apache Shiro 1.2.5 have the AES default key ``kPH+bIxk5D2deZiIxcaaaA==`` in ``org.apache.shiro.mgt.AbstractRememberMeManager``. Shiro components that enable the RememberMe function will allow remote attackers to construct serialized data and execute arbitrary commands on the target server.
