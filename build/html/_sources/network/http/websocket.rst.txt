WebSocket
========================================

Introduction
----------------------------------------
WebSocket is a network transmission protocol that allows full duplex communication on a single TCP connection, located at the application layer of the OSI model. The WebSocket protocol was standardized by IETF to RFC 6455 in 2011, and was later supplemented by RFC 7936.

Interaction
----------------------------------------

handshake
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The handshake phase is similar to the HTTP protocol. The handshake example given in the RFC document is as follows:

::

GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Origin: http://example.com
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13


::

HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-Websocket-Accept: S3PLEPLMLMAQ9KYKZZRBK + XI

The value of Upgrade must be websocket and the value of Connection must be Upgrade, which together means that the client prefers to upgrade to the Websocket protocol.

Sec-WebSocket-Key is a random value, and Sec-WebSocket-Accept is the Base64 encoded value of Sec-WebSocket-Key splicing specific string ``258EAFA5-E914-47DA-95CA-C5AB0DC85B11`` calculates the Base64 encoded value after SHA1 digest. In the example, ``s3pPLMBiTxaQ9kYGzzhZRbK+xOo=` is the corresponding SHA1 summary of ``dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11``.
