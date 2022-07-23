WebSocket
========================================

简介
----------------------------------------
WebSocket是一种网络传输协议，可在单个TCP连接上进行全双工通信，位于OSI模型的应用层。WebSocket协议在2011年由IETF标准化为RFC 6455，后由RFC 7936补充规范。

交互
----------------------------------------

握手
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
握手阶段和 HTTP 协议较为类似，RFC 文档中给出的握手示例如下：

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

其中 Upgrade 的值必须为 websocket ，Connection 的值必须为 Upgrade ，合起来表示客户端喜欢连接升级到 Websocket 协议。

Sec-WebSocket-Key 是一个随机值，Sec-WebSocket-Accept 是 Sec-WebSocket-Key 拼接特定字符串 ``258EAFA5-E914-47DA-95CA-C5AB0DC85B11`` 计算SHA1摘要后的 Base64 编码的值。例子中 ``s3pPLMBiTxaQ9kYGzzhZRbK+xOo=`` 就是 ``dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11`` 对应的SHA1摘要。
