SSL/TLS
========================================

简介
----------------------------------------
SSL全称是Secure Sockets Layer，安全套接字层，它是由网景公司(Netscape)在1994年时设计，主要用于Web的安全传输协议，目的是为网络通信提供机密性、认证性及数据完整性保障。如今，SSL已经成为互联网保密通信的工业标准。

SSL最初的几个版本(SSL 1.0、SSL2.0、SSL 3.0)由网景公司设计和维护，从3.1版本开始，SSL协议由因特网工程任务小组(IETF)正式接管，并更名为TLS(Transport Layer Security)，发展至今已有TLS 1.0、TLS1.1、TLS1.2、TLS1.3这几个版本。

如TLS名字所说，SSL/TLS协议仅保障传输层安全。同时，由于协议自身特性(数字证书机制)，SSL/TLS不能被用于保护多跳(multi-hop)端到端通信，而只能保护点到点通信。

SSL/TLS协议能够提供的安全目标主要包括如下几个：

- 认证性
    - 借助数字证书认证服务端端和客户端身份，防止身份伪造
- 机密性
    - 借助加密防止第三方窃听
- 完整性
    - 借助消息认证码(MAC)保障数据完整性，防止消息篡改
- 重放保护
    - 通过使用隐式序列号防止重放攻击

为了实现这些安全目标，SSL/TLS协议被设计为一个两阶段协议，分为握手阶段和应用阶段：

握手阶段也称协商阶段，在这一阶段，客户端和服务端端会认证对方身份(依赖于PKI体系，利用数字证书进行身份认证)，并协商通信中使用的安全参数、密码套件以及MasterSecret。后续通信使用的所有密钥都是通过MasterSecret生成。
在握手阶段完成后，进入应用阶段。在应用阶段通信双方使用握手阶段协商好的密钥进行安全通信。

协议
----------------------------------------
TLS 包含几个子协议，比较常用的有记录协议、警报协议、握手协议、变更密码规范协议等。

记录协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
记录协议(Record Protocol)规定了 TLS 收发数据的基本单位记录(record)。

警报协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
警报协议(Alert Protocol)用于提示协议交互过程出现错误。

握手协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
握手协议(Handshake Protocol)是 TLS 里最复杂的子协议，在握手过程中协商 TLS 版本号、随机数、密码套件等信息，然后交换证书和密钥参数，最终双方协商得到会话密钥，用于后续的混合加密系统。

变更密码规范协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
变更密码规范协议(Change Cipher Spec Protocol)是一个“通知”，告诉对方，后续的数据都将使用加密保护。

交互过程
----------------------------------------

Client Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Client Hello 由客户端发送，内容包括客户端的一个Unix时间戳(GMT Unix Time)、一些随机的字节(Random Bytes)，还包括了客户端接受的算法类型(Cipher Suites)。

Server Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Server Hello 由服务端发送，内容包括服务端支持的算法类型、GMT Unix Time以及Random Bytes。

Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
由服务端或者客户端发送，发送方会会将自己的数字证书发送给接收方，由接收方进行证书验证，如果不通过的话，接收方会中断握手的过程。一般跟在Client / Server Hello报文之后。

Server Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
由服务端发送，将自己的公钥参数传输给了客户端，一般也和Server Hello与Certificate在一个TCP报文中。

Server Hello Done
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
服务端发送，一般也和Server Hello、Certificate和Server Key Exchange在一个TCP报文中。

Client Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
客户端发送，向服务端发送自己的公钥参数，与服务端协商密钥。

Change Cipher Spec
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
客户端或者服务端发送，紧跟着Key Exchange发送，代表自己生成了新的密钥，通知对方以后将更换密钥，使用新的密钥进行通信。

Encrypted Handshake Message
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
客户端或者服务端发送，紧跟着Key Exchange发送。进行测试，一方用自己的刚刚生成的密钥加密一段固定的消息发送给对方，如果密钥协商正确无误的话，对方可以正确解密。

New Session Ticket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
服务端发送，表示发起会话，在一段时间之内(超时时间到来之前)，双方都以刚刚交换的密钥进行通信。从这以后，加密通信正式开始。

Application Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
使用密钥交换协议协商出来的密钥加密的应用层的数据。

Encrypted Alert
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
客户端或服务端发送，意味着加密通信因为某些原因需要中断，警告对方不要再发送敏感的数据。

版本更新内容
----------------------------------------

TLS 1.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 引入了PSK作为新的密钥协商机制
- 支持 0-RTT 模式，以安全性降低为代价，在建立连接时节省了往返时间
- ServerHello 之后的所有握手消息采取了加密操作，可见明文减少
- 不再允许对加密报文进行压缩、不再允许双方发起重协商
- DSA 证书不再允许在 TLS 1.3 中使用
- 删除不安全的密码算法
    - RSA 密钥传输 - 不支持前向安全性
    - CBC 模式密码 - 易受 BEAST 和 Lucky 13 攻击
    - RC4 流密码 - 在 HTTPS 中使用并不安全
    - SHA-1 哈希函数 - 建议以 SHA-2 取而代之
    - 任意 Diffie-Hellman 组- CVE-2016-0701 漏洞
    - 输出密码 - 易受 FREAK 和 LogJam 攻击

子协议
----------------------------------------
SSL/TLS协议有一个高度模块化的架构，分为很多子协议，主要是：

- Handshake 协议
    - 包括协商安全参数和密码套件、服务端身份认证(客户端身份认证可选)、密钥交换
- ChangeCipherSpec 协议
    - 一条消息表明握手协议已经完成
- Alert 协议
    - 对握手协议中一些异常的错误提醒，分为fatal和warning两个级别，fatal类型的错误会直接中断SSL链接，而warning级别的错误SSL链接仍可继续，只是会给出错误警告
- Record 协议
    - 包括对消息的分段、压缩、消息认证和完整性保护、加密等

参考链接
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 2246 The TLS Protocol Version 1.0 <https://tools.ietf.org/html/rfc2246>`_
- `RFC 4346 The Transport Layer Security (TLS) Protocol Version 1.1 <https://tools.ietf.org/html/rfc4346>`_
- `RFC 5246 The Transport Layer Security (TLS) Protocol Version 1.2 <https://tools.ietf.org/html/rfc5246>`_
- `RFC 6101 The Secure Sockets Layer (SSL) Protocol Version 3.0 <https://tools.ietf.org/html/rfc6101>`_
- `RFC 6176 Prohibiting Secure Sockets Layer (SSL) Version 2.0 <https://tools.ietf.org/html/rfc6176>`_
- `RFC 7568 Deprecating Secure Sockets Layer Version 3.0 <https://tools.ietf.org/html/rfc7568>`_
- `RFC 8446 The Transport Layer Security (TLS) Protocol Version 1.3 <https://tools.ietf.org/html/rfc8446>`_

Document
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Wikipedia Transport Layer Security <https://en.wikipedia.org/wiki/Transport_Layer_Security>`_
