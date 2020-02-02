SAML
========================================

简介
----------------------------------------
SAML (Security Assertion Markup Language) 译为安全断言标记语言，是一种xXML格式的语言，使用XML格式交互，来完成SSO的功能。

SAML存在1.1和2.0两个版本，这两个版本不兼容，不过在逻辑概念或者对象结构上大致相当，只是在一些细节上有所差异。

认证过程
----------------------------------------
SAML的认证涉及到三个角色，分别为服务提供者(SP)、认证服务(IDP)、用户(Client)。一个比较典型认证过程如下：

1. Client访问受保护的资源
2. SP生成认证请求SAML返回给Client
3. Client提交请求到IDP
4. IDP返回认证请求
5. Client登陆IDP
6. 认证成功后，IDP生成私钥签名标识了权限的SAML，返回给Client
7. Client提交SAML给SP
8. SP读取SAML，确定请求合法，返回资源

安全问题
----------------------------------------
- 源于ssl模式下的认证可选性，可以删除签名方式标签绕过认证
- 如果SAML中缺少了expiration，并且断言ID不是唯一的，那么就可能被重放攻击影响

参考链接
----------------------------------------
- `SAML Wiki <https://en.wikipedia.org/wiki/SAML_2.0>`_
- `RFC7522 <https://tools.ietf.org/html/rfc7522>`_
- `SSO Wars The Token Menace <https://i.blackhat.com/USA-19/Wednesday/us-19-Munoz-SSO-Wars-The-Token-Menace.pdf>`_
