OAuth
========================================

Introduction
----------------------------------------
OAuth is an open network standard for authorization and is widely used around the world. The current version is version 2.0.

OAuth sets up an authorization layer between the client and the server. The client cannot log in to the server directly, but can only log in to the authorization layer to distinguish the user from the client. The token used by the client to log in to the authorization layer is different from the user's password. Users can specify the permission scope and validity period of the authorization layer token when logging in.

After the client logs in to the authorization layer, the server opens the user's stored information to the client based on the permission scope and validity period of the token.

OAuth 2.0 defines four authorization methods: authorization code mode, simplified mode (implicit), password mode (resource owner password credentials) and client mode (client credentials).

process
----------------------------------------
- After the user opens the client, the client requires the user to authorize
- The user agrees to authorize the client
- The client uses the authorization obtained in the previous step to apply for a token from the authentication server
- After the authentication server authenticates the client, it confirms that it is correct and agrees to issue the token.
- The client uses the token to apply to the resource server to obtain resources
- The resource server confirms that the token is correct and agrees to open resources to the client

Authorization code mode
----------------------------------------
Authorization code mode is the authorization mode with the most complete functions and the strictest process. Its characteristic is that it interacts with the server's authentication server through the client's backend server.

The process is:

- The user accesses the client, which directs the former to the authentication server
- The user chooses whether to authorize the client
- Assuming that the user grants authorization, the authentication server directs the user to the "redirection URI" specified by the client in advance, and attaches an authorization code.
- The client receives the authorization code, attaches the earlier "redirect URI", and applies for a token from the authentication server
- The authentication server checks the authorization code and redirect URI. After confirming that they are correct, it sends the access token and refresh token to the client.

In step A, the URI used by the client to apply for authentication includes the following parameters:

- response_type: Indicates the authorization type, required. The value here is fixed to ``code``
- client_id: Indicates the ID of the client, required
- redirect_uri: Represents redirect URI, optional
- Scope: Indicates the scope of permissions applied for, optional
- state: Indicates the current state of the client, which needs to be specified dynamically to prevent CSRF

For example:

::

    GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com

In step C, the server responds to the client's URI, including the following parameters:

- code: indicates the authorization code, required. The validity period of the code should be short and the client can only use the code once, otherwise it will be rejected by the authorization server. This code has a one-to-one correspondence with the client ID and redirect URI.
- state: If the client's request contains this parameter, the authentication server responds with the same parameters as the request.

For example:

::

    HTTP/1.1 302 Found
    Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz

In step D, the client applies for an HTTP request for a token from the authentication server, including the following parameters:

- grant_type: Indicates the authorization mode used, required. The value here is fixed to ``authorization_code``
- code: indicates the authorization code obtained in the previous step, required
- redirect_uri: Represents the redirect URI, required, and must be consistent with the parameter value in step A
- client_id: represents the client ID, required

For example:

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb


In step E, the HTTP reply sent by the authentication server contains the following parameters:

- access_token: indicates access token, required
- token_type: Indicates the token type. The value is case-insensitive and required. It can be the ``bearer`` type or the ``mac`` type.
- expires_in: Indicates the expiration time, in seconds. If this parameter is omitted, the expiration time must be set in other ways
- refresh_token: Represents an update token, used to obtain the next access token, optional
- Scope: Indicates the scope of authority. If it is consistent with the scope applied by the client, this item can be omitted.

For example:

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

Simplified mode
----------------------------------------
Simplified mode (implicit grant type) does not go through the third-party application server, but directly applies for a token from the authentication server in the browser, skipping the authorization code step, hence the name. All steps are completed in the browser, the token is visible to visitors, and no authentication is required on the client side.

The steps are:

- The client directs the user to the authentication server
- The user decides whether to grant authorization to the client
- Assuming the user grants authorization, the authentication server directs the user to the redirect URI specified by the client, and includes the access token in the Hash part of the URI
- The browser sends a request to the resource server, which does not include the Hash value received in the previous step.
- The resource server returns a web page that contains code to obtain the token in the hash value
- The browser executes the script obtained in the previous step and extracts the token
- The browser sends the token to the client

In step A, the HTTP request sent by the client contains the following parameters:

- response_type: Indicates the authorization type, the value here is fixed to ``token``, required
- client_id: Indicates the ID of the client, required
- redirect_uri: Represents the URI of redirection, optional
- Scope: Indicates the scope of authority, optional
- state: Indicates the current state of the client, which needs to be specified dynamically to prevent CSRF

For example:

::

    GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com

In step C, the authentication server responds to the client's URI, including the following parameters:

- access_token: indicates access token, required
- token_type: Indicates the token type. This value is not case sensitive and is required.
- expires_in: Indicates the expiration time, in seconds. If this parameter is omitted, the expiration time must be set in other ways
- Scope: Indicates the scope of authority. If it is consistent with the scope applied by the client, this item can be omitted.
- state: If the client's request contains this parameter, the authentication server responds with the same parameters as the request.

For example:

::

     HTTP/1.1 302 Found
     Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA&state=xyz&token_type=example&expires_in=3600

In the above example, the authentication server uses the Location field of the HTTP header to specify the URL to which the browser redirects. Note that the hash portion of this URL contains the token.

According to step D above, the browser will access the URL specified by Location in the next step, but the Hash part will not be sent. In the next step E, the code sent by the service provider's resource server will extract the token in the Hash.

password mode
----------------------------------------
In password mode (Resource Owner Password Credentials Grant), users provide their username and password to the client. The client uses this information to request authorization from the "service provider".

In this mode, the user must give his or her password to the client, but the client must not store the password.

The steps are as follows:

- User provides username and password to client
- The client sends the username and password to the authentication server and requests a token from the latter
- After the authentication server confirms that it is correct, it provides the access token to the client

In step B, the HTTP request sent by the client contains the following parameters:

- grant_type: indicates the authorization type, the value here is fixed to ``password``, required
- username: indicates user name, required
- password: indicates the user's password, required
- Scope: Indicates the scope of authority, optional

For example:

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=password&username=johndoe&password=A3ddj3w

In step C, the authentication server sends the access token to the client, for example:

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


client mode
----------------------------------------
Client mode (Client Credentials Grant) means that the client authenticates to the server in its own name, not in the name of the user.

The steps are as follows:

- The client authenticates to the authentication server and requires an access token
- After the authentication server confirms that it is correct, it provides the access token to the client

In step A, the HTTP request sent by the client contains the following parameters:

- granttype: Indicates the authorization type, the value here is fixed to ``clientcredentials``, required
- Scope: Indicates the scope of authority, optional

For example:

::

    POST /token HTTP/1.1
    Host: server.example.com
    Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
    Content-Type: application/x-www-form-urlencoded

    grant_type=client_credentials

In step B, the authentication server sends the access token to the client, for example:

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

Reference link
----------------------------------------
- `rfc6749 <http://www.rfcreader.com/#rfc6749>`_
- `Understanding OAuth <http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html>`_
- `OAuth 2.0 Vulnerabilities <https://ldapwiki.com/wiki/OAuth%202.0%20Vulnerabilities>`_
- `OAuth Community Site <https://oauth.net/>`_
- `Hidden OAuth attack vectors <https://portswigger.net/research/hidden-oauth-attack-vectors>`_
