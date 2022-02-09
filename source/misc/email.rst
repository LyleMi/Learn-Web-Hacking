邮件安全
========================================

常用概念
----------------------------------------
邮件安全常用的概念是SPF、DKIM和DMARC。其中 SPF (Sender Policy Framework) 是一条特殊的DNS记录，用于设定合法的发送邮件的IP。

DKIM (DomainKeys Identified Mail) 将数字签名添加到电子邮件消息的标题中，使邮件服务器拥有确保邮件内容没有更改的能力，同样DKIM也存在于DNS中。通过查询 ``<selector>._domainkey.example.com`` 的txt记录查询。

DMARC(Domain-based Message Authentication): 通过查询 ``<selector>._domainkey.example.com`` 的txt记录查询。
