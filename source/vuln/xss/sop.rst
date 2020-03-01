同源策略
========================================

简介
----------------------------------------
同源策略限制了不同源之间如何进行资源交互，是用于隔离潜在恶意文件的重要安全机制。
是否同源由URL决定，URL由协议、域名、端口和路径组成，如果两个URL的协议、域名和端口相同，则表示他们同源。

file域的同源策略
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在之前的浏览器中，任意两个file域的URI被认为是同源的。本地磁盘上的任何HTML文件都可以读取本地磁盘上的任何其他文件。

从Gecko 1.9开始，文件使用了更细致的同源策略，只有当源文件的父目录是目标文件的祖先目录时，文件才能读取另一个文件。

cookie的同源策略
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cookie使用不同的源定义方式，一个页面可以为本域和任何父域设置cookie，只要是父域不是公共后缀（public suffix）即可。

不管使用哪个协议（HTTP/HTTPS）或端口号，浏览器都允许给定的域以及其任何子域名访问cookie。设置 cookie时，可以使用 ``domain`` / ``path`` / ``secure`` 和 ``http-only`` 标记来限定其访问性。

所以 ``https://localhost:8080/`` 和 ``http://localhost:8081/`` 的Cookie是共享的。

Flash/SilverLight跨域
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
浏览器的各种插件也存在跨域需求。通常是通过在服务器配置crossdomain.xml，设置本服务允许哪些域名的跨域访问。

客户端会请求此文件，如果发现自己的域名在访问列表里，就发起真正的请求，否则不发送请求。

源的更改
----------------------------------------
同源策略认为域和子域属于不同的域，例如 ``child1.a.com`` 与 ``a.com`` / ``child1.a.com`` 与 ``child2.a.com`` / ``xxx.child1.a.com`` 与 ``child1.a.com`` 两两不同源。

对于这种情况，可以在两个方面各自设置 ``document.domain='a.com'`` 来改变其源来实现以上任意两个页面之间的通信。

另外因为浏览器单独保存端口号，这种赋值会导致端口号被重写为 ``null`` 。

跨源访问
----------------------------------------
同源策略控制了不同源之间的交互，这些交互通常分为三类：

+ 通常允许跨域写操作（Cross-origin writes）
    + 链接（links）
    + 重定向
    + 表单提交
+ 通常允许跨域资源嵌入（Cross-origin embedding）
+ 通常不允许跨域读操作（Cross-origin reads）

可能嵌入跨源的资源的一些示例有：

+ ``<script src="..."></script>`` 标签嵌入跨域脚本。语法错误信息只能在同源脚本中捕捉到。
+ ``<link rel="stylesheet" href="...">`` 标签嵌入CSS。由于CSS的松散的语法规则，CSS的跨域需要一个设置正确的Content-Type 消息头。
+ ``<img>`` / ``<video>`` / ``<audio>`` 嵌入多媒体资源。
+ ``<object>`` ``<embed>`` 和 ``<applet>`` 的插件。
+ ``@font-face`` 引入的字体。一些浏览器允许跨域字体（ cross-origin fonts），一些需要同源字体（same-origin fonts）。
+ ``<frame>`` 和 ``<iframe>`` 载入的任何资源。站点可以使用X-Frame-Options消息头来阻止这种形式的跨域交互。

JSONP跨域
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
JSONP就是利用 ``<script>`` 标签的跨域能力实现跨域数据的访问，请求动态生成的JavaScript脚本同时带一个callback函数名作为参数。

服务端收到请求后，动态生成脚本产生数据，并在代码中以产生的数据为参数调用callback函数。

JSONP也存在一些安全问题，例如当对传入/传回参数没有做校验就直接执行返回的时候，会造成XSS问题。没有做Referer或Token校验就给出数据的时候，可能会造成数据泄露。

另外JSONP在没有设置callback函数的白名单情况下，可以合法的做一些设计之外的函数调用，引入问题。这种攻击也被称为SOME攻击。

跨源脚本API访问
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Javascript的APIs中，如 ``iframe.contentWindow`` , ``window.parent``, ``window.open`` 和 ``window.opener`` 允许文档间相互引用。当两个文档的源不同时，这些引用方式将对 ``window`` 和 ``location`` 对象的访问添加限制。

``window`` 允许跨源访问的方法有

- window.blur
- window.close
- window.focus
- window.postMessage

``window`` 允许跨源访问的属性有

- window.closed
- window.frames
- window.length
- window.location
- window.opener
- window.parent
- window.self
- window.top
- window.window

其中 ``window.location`` 允许读/写，其他的属性只允许读

跨源数据存储访问
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
存储在浏览器中的数据，如 ``localStorage`` 和 ``IndexedDB``，以源进行分割。每个源都拥有自己单独的存储空间，一个源中的Javascript脚本不能对属于其它源的数据进行读写操作。

CORS
----------------------------------------
CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。通过这个标准，可以允许浏览器读取跨域的资源。

常见请求头
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Origin
    - 预检请求或实际请求的源站URI, 浏览器请求默认会发送该字段
    - ``Origin: <origin>``
- Access-Control-Request-Method
    - 声明请求使用的方法
    - ``Access-Control-Request-Method: <method>``
- Access-Control-Request-Headers
    - 声明请求使用的header字段
    - ``Access-Control-Request-Headers: <field-name>[, <field-name>]*``

常见返回头
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Access-Control-Allow-Origin
    - 声明允许访问的源外域URI
    - 对于携带身份凭证的请求不可使用通配符 ``*``
    - ``Access-Control-Allow-Origin: <origin> | *``
- Access-Control-Expose-Headers
    - 声明允许暴露的头
    - e.g. ``Access-Control-Expose-Headers: X-My-Custom-Header, X-Another-Custom-Header``
- Access-Control-Max-Age
    - 声明Cache时间
    - ``Access-Control-Max-Age: <delta-seconds>``
- Access-Control-Allow-Credentials
    - 声明是否允许在请求中带入
    - ``Access-Control-Allow-Credentials: true``
- Access-Control-Allow-Methods
    - 声明允许的访问方式
    - ``Access-Control-Allow-Methods: <method>[, <method>]*``
- Access-Control-Allow-Headers
    - 声明允许的头
    - ``Access-Control-Allow-Headers: <field-name>[, <field-name>]*``

防御建议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 如非必要不开启CORS
- 定义详细的白名单，不使用通配符，仅配置所需要的头
- 配置 ``Vary: Origin`` 头部
- 如非必要不使用 ``Access-Control-Allow-Credentials``
- 限制缓存的时间

阻止跨源访问
----------------------------------------
阻止跨域写操作，可以检测请求中的 ``CSRF token`` ，这个标记被称为Cross-Site Request Forgery (CSRF) 标记。

阻止资源的跨站读取，因为嵌入资源通常会暴露信息，需要保证资源是不可嵌入的。但是多数情况下浏览器都不会遵守 ``Content-Type`` 消息头。例如如果在HTML文档中指定 ``<script>`` 标记，则浏览器会尝试将HTML解析为JavaScript。 
