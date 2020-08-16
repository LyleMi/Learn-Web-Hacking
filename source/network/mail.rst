邮件协议族
========================================

简介
----------------------------------------

SMTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SMTP (Simple Mail Transfer Protocol) 是一种电子邮件传输的协议，是一组用于从源地址到目的地址传输邮件的规范。不启用SSL时端口号为25，启用SSL时端口号多为465或994。

POP3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
POP3 (Post Office Protocol 3) 用于支持使用客户端远程管理在服务器上的电子邮件。不启用SSL时端口号为110，启用SSL时端口号多为995。

IMAP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
IMAP (Internet Mail Access Protocol)，即交互式邮件存取协议，它是跟POP3类似邮件访问标准协议之一。不同的是，开启了IMAP后，您在电子邮件客户端收取的邮件仍然保留在服务器上，同时在客户端上的操作都会反馈到服务器上，如：删除邮件，标记已读等，服务器上的邮件也会做相应的动作。不启用SSL时端口号为143，启用SSL时端口号多为993。

防护策略
----------------------------------------

SPF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
发件人策略框架 (Sender Policy Framework, SPF) 是一套电子邮件认证机制，用于确认电子邮件是否由网域授权的邮件服务器寄出，防止有人伪冒身份网络钓鱼或寄出垃圾邮件。SPF允许管理员设定一个DNS TXT记录或SPF记录设定发送邮件服务器的IP范围，如有任何邮件并非从上述指明授权的IP地址寄出，则很可能该邮件并非确实由真正的寄件者寄出。

DKIM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
域名密钥识别邮件 (DomainKeys Identified Mail, DKIM) 是一种检测电子邮件发件人地址伪造的方法。发送方会在邮件的头中插入DKIM-Signature，收件方通过查询DNS记录中的公钥来验证发件人的信息。

DMARC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
基于网域的消息认证、报告和一致性 (Domain-based Message Authentication, Reporting and Conformance, DMARC) 是电子邮件身份验证协议，用于解决在邮件栏中显示的域名和验证的域名不一致的问题。要通过 DMARC 检查，必须通过 SPF 或/和 DKIM 的身份验证，且需要标头地址中的域名必须与经过身份验证的域名一致。

参考链接
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 4408 Sender Policy Framework (SPF) for Authorizing Use of Domains in E-Mail, Version 1 <https://tools.ietf.org/html/rfc4408>`_
- `RFC 6376 DomainKeys Identified Mail (DKIM) Signatures <https://tools.ietf.org/html/rfc6376>`_
- `RFC 7208 Sender Policy Framework (SPF) for Authorizing Use of Domains in Email, Version 1 <https://tools.ietf.org/html/rfc7208>`_
- `RFC 7489 Domain-based Message Authentication, Reporting, and Conformance (DMARC) <https://tools.ietf.org/html/rfc7489>`_
- `RFC 8301 Cryptographic Algorithm and Key Usage Update to DomainKeys Identified Mail (DKIM) <https://tools.ietf.org/html/rfc8301>`_
- `RFC 8463 A New Cryptographic Signature Method for DomainKeys Identified Mail (DKIM) <https://tools.ietf.org/html/rfc8463>`_
- `RFC 8616 Email Authentication for Internationalized Mail <https://tools.ietf.org/html/rfc8616>`_
- `RFC 8611 Mail <https://tools.ietf.org/html/rfc8611>`_

相关文档
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Sender Policy Framework wikipedia <https://en.wikipedia.org/wiki/Sender_Policy_Framework>`_
- `DomainKeys Identified Mail wikipedia <https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail>`_
- `DMARC wikipedia <https://en.wikipedia.org/wiki/DMARC>`_

研究文章
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Composition Kills:A Case Study of Email Sender Authentication <http://i.blackhat.com/USA-20/Thursday/us-20-Chen-You-Have-No-Idea-Who-Sent-That-Email-18-Attacks-On-Email-Sender-Authentication-wp.pdf>`_
