HTTP Version
========================================

HTTP
----------------------------------------
HTTP is an application-layer protocol based on the TCP/IP protocol. It mainly specifies the communication format between the client and the server, and uses port 80 by default.

HTTP 0.9
----------------------------------------
HTTP 0.9 was first released in 1991 and only supports GET commands. The request format is only a simple ``GET /url`` . The server only responds to HTML and closes the TCP connection after the response is completed.

HTTP 1.0
----------------------------------------
In May 1996, the HTTP/1.0 version was released, enriching the format and content of the transmission, and introducing two verbs POST and HEAD. Starting from 1.0, a protocol version must be added at the tail. In 1.0, status code, multi-character set support, multi-part type, authorization, cache, content encoding, etc. are also introduced.

The main disadvantage of HTTP version 1.0 is that only one request can be sent per TCP connection. After sending the data, the connection is closed. If you want to request other resources, you must create another connection.

The cost of creating a new TCP connection is very high because the client and server need to shake hands three times, and the sending rate is slow start at the beginning, so the performance of HTTP 1.0 version is relatively poor.

HTTP 1.1
----------------------------------------
In January 1997, the HTTP/1.1 version was released, further improving the HTTP protocol. Version 1.1 mainly introduces persistent connections, pipeline mechanisms, Content-Length, block transmission encoding and other contents. The pipeline mechanism is that in the same TCP connection, the client can send multiple requests at the same time, which improves the efficiency of the HTTP protocol. Verb methods such as PUT, PATCH, HEAD, OPTIONS, DELETE, etc. were also introduced in HTTP 1.1 version. In addition, the Host field was added in version 1.1 to specify the domain name of the server, which is also the basis for the development of virtual hosts later.

Although version 1.1 allows multiplexing of TCP connections, all data communications in the same TCP connection are carried out in order. The server will only make the next response after processing one response. If there is a request that is very slow, it will block the subsequent request.

Spdy
----------------------------------------
In 2009, Google disclosed its own SPDY protocol to solve the problem of low HTTP/1.1 efficiency, and was then used as the basis of HTTP/2.

HTTP/2
----------------------------------------
In 2015, HTTP/2 was released. HTTP/2 is a binary protocol. The header information and data body are both binary, collectively called frames. The frames are divided into header information frames and data frames. HTTP/2 Multiplexing TCP connections. In one connection, both the client and the browser can send multiple requests or responses at the same time, without responding in sequence.
