OAuth
========================================

简介
----------------------------------------
OAuth是一个关于授权（authorization）的开放网络标准，在全世界得到广泛应用，目前的版本是2.0版。

OAuth在客户端与服务端之间，设置了一个授权层（authorization layer）。客户端不能直接登录服务端，只能登录授权层，以此将用户与客户端区分开来。客户端登录授权层所用的令牌（token），与用户的密码不同。用户可以在登录的时候，指定授权层令牌的权限范围和有效期。

客户端登录授权层以后，服务端根据令牌的权限范围和有效期，向客户端开放用户储存的资料。

OAuth 2.0定义了四种授权方式：授权码模式（authorization code）、简化模式（implicit）、密码模式（resource owner password credentials）和客户端模式（client credentials）。

流程
----------------------------------------
- 用户打开客户端以后，客户端要求用户给予授权
- 用户同意给予客户端授权
- 客户端使用上一步获得的授权，向认证服务器申请令牌
- 认证服务器对客户端进行认证以后，确认无误，同意发放令牌
- 客户端使用令牌，向资源服务器申请获取资源
- 资源服务器确认令牌无误，同意向客户端开放资源

授权码模式
----------------------------------------
授权码模式（authorization code）是功能最完整、流程最严密的授权模式。它的特点就是通过客户端的后台服务器，与服务端的认证服务器进行互动。

其流程为：

- 用户访问客户端，后者将前者导向认证服务器
- 用户选择是否给予客户端授权
- 假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI） ，同时附上一个授权码
- 客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌
- 认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）

A步骤中，客户端申请认证的URI，包含以下参数：

- response_type：表示授权类型，必选项，此处的值固定为 ``code``
- client_id：表示客户端的ID，必选项
- redirect_uri：表示重定向URI，可选项
- scope：表示申请的权限范围，可选项
- state：表示客户端的当前状态，需动态指定，防止CSRF

例如：

::

    GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com

C步骤中，服务器回应客户端的URI，包含以下参数：

- code：表示授权码，必选项。该码的有效期应该很短且客户端只能使用该码一次，否则会被授权服务器拒绝。该码与客户端ID和重定向URI，是一一对应关系。
- state：如果客户端的请求中包含这个参数，认证服务器回应与请求时相同的参数

例如：

::

    HTTP/1.1 302 Found
    Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz

D步骤中，客户端向认证服务器申请令牌的HTTP请求，包含以下参数：

- grant_type：表示使用的授权模式，必选项，此处的值固定为 ``authorization_code``
- code：表示上一步获得的授权码，必选项
- redirect_uri：表示重定向URI，必选项，且必须与A步骤中的该参数值保持一致
- client_id：表示客户端ID，必选项

例如：

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb


E步骤中，认证服务器发送的HTTP回复，包含以下参数：

- access_token：表示访问令牌，必选项
- token_type：表示令牌类型，该值大小写不敏感，必选项，可以是 ``bearer`` 类型或 ``mac`` 类型
- expires_in：表示过期时间，单位为秒。如果省略该参数，必须其他方式设置过期时间
- refresh_token：表示更新令牌，用来获取下一次的访问令牌，可选项
- scope：表示权限范围，如果与客户端申请的范围一致，此项可省略

例如：

::

     HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"2YotnFZFEjr1zCsicMWpAA",
       "token_type":"example",
       "expires_in":3600,
       "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
       "example_parameter":"example_value"
     }

简化模式
----------------------------------------
简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了授权码这个步骤，因此得名。所有步骤在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。

其步骤为：

- 客户端将用户导向认证服务器
- 用户决定是否给于客户端授权
- 假设用户给予授权，认证服务器将用户导向客户端指定的重定向URI，并在URI的Hash部分包含了访问令牌
- 浏览器向资源服务器发出请求，其中不包括上一步收到的Hash值
- 资源服务器返回一个网页，其中包含的代码可以获取Hash值中的令牌
- 浏览器执行上一步获得的脚本，提取出令牌
- 浏览器将令牌发给客户端

A步骤中，客户端发出的HTTP请求，包含以下参数：

- response_type：表示授权类型，此处的值固定为 ``token`` ，必选项
- client_id：表示客户端的ID，必选项
- redirect_uri：表示重定向的URI，可选项
- scope：表示权限范围，可选项
- state：表示客户端的当前状态，需动态指定，防止CSRF

例如：

::

    GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com

C步骤中，认证服务器回应客户端的URI，包含以下参数：

- access_token：表示访问令牌，必选项
- token_type：表示令牌类型，该值大小写不敏感，必选项
- expires_in：表示过期时间，单位为秒。如果省略该参数，必须其他方式设置过期时间
- scope：表示权限范围，如果与客户端申请的范围一致，此项可省略
- state：如果客户端的请求中包含这个参数，认证服务器回应与请求时相同的参数

例如：

::

     HTTP/1.1 302 Found
     Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA&state=xyz&token_type=example&expires_in=3600

在上面的例子中，认证服务器用HTTP头信息的Location栏，指定浏览器重定向的网址。注意，在这个网址的Hash部分包含了令牌。

根据上面的D步骤，下一步浏览器会访问Location指定的网址，但是Hash部分不会发送。接下来的E步骤，服务提供商的资源服务器发送过来的代码，会提取出Hash中的令牌。

密码模式
----------------------------------------
密码模式（Resource Owner Password Credentials Grant）中，用户向客户端提供自己的用户名和密码。客户端使用这些信息，向"服务商提供商"索要授权。

在这种模式中，用户必须把自己的密码给客户端，但是客户端不得储存密码。

其步骤如下：

- 用户向客户端提供用户名和密码
- 客户端将用户名和密码发给认证服务器，向后者请求令牌
- 认证服务器确认无误后，向客户端提供访问令牌

B步骤中，客户端发出的HTTP请求，包含以下参数：

- grant_type：表示授权类型，此处的值固定为 ``password`` ，必选项
- username：表示用户名，必选项
- password：表示用户的密码，必选项
- scope：表示权限范围，可选项

例如：

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=password&username=johndoe&password=A3ddj3w

C步骤中，认证服务器向客户端发送访问令牌，例如：

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "access_token": "2YotnFZFEjr1zCsicMWpAA",
        "token_type": "example",
        "expires_in": 3600,
        "refresh_token": "tGzv3JOkF0XG5Qx2TlKWIA",
        "example_parameter": "example_value"
    }


客户端模式
----------------------------------------
客户端模式（Client Credentials Grant）指客户端以自己的名义，而不是以用户的名义，向服务端进行认证。

其步骤如下：

- 客户端向认证服务器进行身份认证，并要求一个访问令牌
- 认证服务器确认无误后，向客户端提供访问令牌

A步骤中，客户端发出的HTTP请求，包含以下参数：

- granttype：表示授权类型，此处的值固定为 ``clientcredentials`` ，必选项
- scope：表示权限范围，可选项

例如：

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=client_credentials

B步骤中，认证服务器向客户端发送访问令牌，例如：

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "access_token": "2YotnFZFEjr1zCsicMWpAA",
        "token_type": "example",
        "expires_in": 3600,
        "example_parameter": "example_value"
    }

参考链接
----------------------------------------
- `rfc6749 <http://www.rfcreader.com/#rfc6749>`_
- `理解OAuth <http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html>`_
- `OAuth 2.0 Vulnerabilities <https://ldapwiki.com/wiki/OAuth%202.0%20Vulnerabilities>`_
- `OAuth Community Site <https://oauth.net/>`_
- `Hidden OAuth attack vectors <https://portswigger.net/research/hidden-oauth-attack-vectors>`_
