认证方式
================================

JWT (JSON Web Token)
--------------------------------

Json web token (JWT), 是为了在网络应用环境间传递声明而执行的一种基于JSON的开放标准（(RFC 7519).该token被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源，也可以增加一些额外的其它业务逻辑所必须的声明信息，该token也可直接被用于认证，也可被加密。

构成
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
分为三个部分，分别为header/payload/signature。其中header是声明的类型和加密使用的算法。payload是载荷，最后是加上 ``HMAC(base64(header)+base64(payload), secret)``

攻击
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 修改算法为none
- 修改算法RS256为HS256
- 弱密钥破解

参考链接
--------------------------------
- `Critical vulnerabilities in JSON Web Token libraries <https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/>`_