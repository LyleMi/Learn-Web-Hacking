HTTP version
========================================

HTTP
----------------------------------------
HTTP is an application layer protocol based on the TCP/IP protocol. It mainly specifies the communication format between the client and the server. Port 80 is used by default.

HTTP 0.9
----------------------------------------
HTTP 0.9 was first released in 1991. It only supports GET commands. The request format is only simple ``GET /url``. The server only responds to HTML and closes the TCP connection after the response is completed.

HTTP 1.0
----------------------------------------
In May 1996, HTTP/1.0 version was released, which enriched the format and content of transmission and introduced two verbs, POST and HEAD. Starting from 1.0, the protocol version must be added at the end. In 1.0, status code, multi-character set support, multi-part type, authorization, cache, content encoding and other contents were also introduced.

The main disadvantage of HTTP version 1.0 is that only one request can be sent per TCP connection. After sending the data, the connection is closed. If you want to request other resources, you must create a new connection.

The cost of establishing a TCP connection is high because it requires a three-way handshake between the client and the server, and the sending rate is slow at the beginning (slow start). Therefore, the performance of the HTTP 1.0 version is relatively poor.

HTTP 1.1
----------------------------------------
In January 1997, HTTP/1.1 version was released, further improving the HTTP protocol. Version 1.1 mainly introduces persistent connections, pipeline mechanisms, Content-Length, chunked transfer encoding, etc. The pipeline mechanism means that in the same TCP connection, the client can send multiple requests at the same time, thus improving the efficiency of the HTTP protocol. Verb methods such as PUT, PATCH, HEAD, OPTIONS, and DELETE were also introduced in HTTP version 1.1. In addition, version 1.1 added a Host field, which is used to specify the domain name of the server. This is also the basis for the later development of virtual hosts.

Although version 1.1 allows reuse of TCP connections, all data communications within the same TCP connection are performed in sequence. The server will not proceed to the next response until it has processed one response. If one request is slow, subsequent requests will be blocked.

SPDY
----------------------------------------
In 2009, Google disclosed its self-developed SPDY protocol to solve the problem of low efficiency of HTTP/1.1, which was later used as the basis of HTTP/2.

HTTP/2
----------------------------------------
In 2015, HTTP/2 was released. HTTP/2 is a binary protocol. The header information and data body are both binary, collectively called a frame. The frame is divided into a header information frame and a data frame. HTTP/2 reuses TCP connections. In one connection, both the client and the browser can send multiple requests or responses at the same time, and do not need to respond in order.
