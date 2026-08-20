WebSocket
========================================

Introduction
----------------------------------------
WebSocket is a network transport protocol that enables full-duplex communication over a single TCP connection and is located at the application layer of the OSI model. The WebSocket protocol was standardized by the IETF as RFC 6455 in 2011, and later supplemented by RFC 7936.

interaction
----------------------------------------

shake hands
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
    Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=

The value of Upgrade must be websocket and the value of Connection must be Upgrade. Together they indicate that the client likes to upgrade the connection to the Websocket protocol.

Sec-WebSocket-Key is a random value, and Sec-WebSocket-Accept is the Base64-encoded value of Sec-WebSocket-Key concatenated with a specific string ``258EAFA5-E914-47DA-95CA-C5AB0DC85B11`` after calculating the SHA1 digest. In the example, ``s3pPLMBiTxaQ9kYGzzhZRbK+xOo=`` is the SHA1 digest corresponding to ``dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11``.
