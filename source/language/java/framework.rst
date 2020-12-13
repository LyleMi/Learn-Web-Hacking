框架
========================================

Servlet
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Servlet(Server Applet)是Java Servlet的简称，称为小服务程序或服务连接器，是用Java编写的服务器端程序，主要功能在于交互式地浏览和修改数据，生成动态Web内容。

狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。Servlet运行于支持Java的应用服务器中。从原理上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。

生命周期为
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 客户端请求该 Servlet
- 加载 Servlet 类到内存
- 实例化并调用init()方法初始化该 Servlet
- service()(根据请求方法不同调用 ``doGet()`` / ``doPost()`` / ... / ``destroy()``

接口
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``init()`` 

在 Servlet 的生命期中，仅执行一次 init() 方法，在服务器装入 Servlet 时执行。

``service()``

service() 方法是 Servlet 的核心。每当一个客户请求一个HttpServlet对象，该对象的 ``service()`` 方法就要被调用，而且传递给这个方法一个"请求"(ServletRequest)对象和一个"响应"(ServletResponse)对象作为参数。

Struts 2
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Struts2是一个基于MVC设计模式的Web应用框架，它本质上相当于一个servlet，在MVC设计模式中，Struts2作为控制器(Controller)来建立模型与视图的数据交互。

请求流程
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 客户端发送请求的tomcat服务器
- 请求经过一系列过滤器
- FilterDispatcher调用ActionMapper来决定这个请求是否要调用某个Action
- ActionMppaer决定调用某个ActionFilterDispatcher把请求给ActionProxy
- ActionProxy通过Configuration Manager查看structs.xml，找到对应的Action类
- ActionProxy创建一个ActionInvocation对象
- ActionInvocation对象回调Action的execute方法
- Action执行完毕后，ActionInvocation根据返回的字符串，找到相应的result，通过HttpServletResponse返回给服务器

相关CVE
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

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring一般指的是Spring Framework，一个轻量级Java应用程序开源框架，提供了简易的开发方式。

Spring MVC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring MVC根据Spring的模式设计的MVC框架，主要用于开发Web应用，简化开发。

Spring Boot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Spring在推出之初方案较为繁琐，因此提供了Spring Boot作为自动化配置工具，降低项目搭建的复杂度。

请求流程
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 用户发送请求给服务器
- 服务器收到请求，使用DispatchServlet处理
- Dispatch使用HandleMapping检查url是否有对应的Controller，如果有，执行
- 如果Controller返回字符串，ViewResolver将字符串转换成相应的视图对象
- DispatchServlet将视图对象中的数据，输出给服务器
- 服务器将数据输出给客户端

CVE概览
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2018-1270
    - Spring Websocket 远程代码执行漏洞
    - Spring Framework 5.0 - 5.0.5
    - Spring Framework 4.3 - 4.3.15
- CVE-2018-1273
    - Spring Data 远程代码执行漏洞
    - Spring Data Commons 1.13 - 1.13.10
    - Spring Data Commons 2.0 - 2.0.5
    - Spring Data REST 2.6 - 2.6.10
    - Spring Data REST 3.0 - 3.0.5
- CVE-2017-8046
    - Spring Data REST 远程代码执行漏洞
- CVE-2017-4971
    - Spring Web Flow 远程代码执行漏洞

Shiro
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro是一个功能强大且易于使用的Java安全框架，功能包括身份验证，授权，加密和会话管理。

CVE概览
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2020-13933  
    - Apache Shiro < 1.6.0
    - 身份验证绕过漏洞
- CVE-2020-11989
    - SHIRO-782 
    - Apache Shiro < 1.5.3
    - 身份验证绕过漏洞
- CVE-2020-1957
    - SHIRO-682
    - Apache Shiro < 1.5.2
    - 身份验证绕过漏洞
- CVE-2019-12422
    - SHIRO-721
    - Apache Shiro < 1.4.2
    - Padding Oracle Attack 远程代码执行漏洞
- CVE-2016-4437
    - SHIRO-550
    - Apache Shiro <= 1.2.4
    - 反序列化远程代码执行漏洞
- CVE-2014-0074
    - SHIRO-460 
    - Apache Shiro < 1.2.3
    - 身份验证绕过漏洞

CVE-2020-13933
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro 1.6.0之前的版本，由于Shiro拦截器与requestURI的匹配流程与Web框架的拦截器的匹配流程有差异，攻击者构造一个特殊的http请求，可以绕过Shiro的认证，未授权访问敏感路径。

CVE-2020-11989
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro 1.5.3之前的版本，由于Shiro拦截器与requestURI的匹配流程与Web框架的拦截器的匹配流程有差异，攻击者构造一个特殊的http请求，可以绕过Shiro的认证，未授权访问敏感路径。此漏洞存在两种攻击方式。

CVE-2020-1957
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro 1.5.2之前的版本，由于Shiro拦截器与requestURI的匹配流程与Web框架的拦截器的匹配流程有差异，攻击者构造一个特殊的http请求，可以绕过Shiro的认证，未授权访问敏感路径。

CVE-2019-12422
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro 1.4.2之前的版本默认使用 ``AES/CBC/PKCS5Padding`` 模式加密,开启RememberMe功能的Shiro组件将允许远程攻击者构造序列化数据，通过Padding Oracle Attack进行爆破，即使在秘钥未知的条件下，也可以在目标服务器上执行任意命令。

CVE-2016-4437
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Shiro 1.2.5之前的版本在 ``org.apache.shiro.mgt.AbstractRememberMeManager`` 中存在AES默认秘钥 ``kPH+bIxk5D2deZiIxcaaaA==`` ，开启RememberMe功能的Shiro组件将允许远程攻击者构造序列化数据，在目标服务器上执行任意命令。
