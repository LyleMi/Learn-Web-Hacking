OAuth
========================================

Introduction
----------------------------------------
OAuth is an open network standard about authorization, which is widely used around the world. The current version is version 2.0.

OAuth sets up an authorization layer between the client and the server. The client cannot log in to the server directly, but can only log in to the authorization layer to distinguish users from the client. The token used by the client to log in to the authorization layer is different from the user's password. When logging in, users can specify the permission range and validity period of the authorization layer token.

After the client logs into the authorization layer, the server opens the user-stored information to the client based on the permission scope and validity period of the token.

OAuth 2.0 defines four authorization methods: authorization code, simplicit, resource owner password credentials and client credentials.

process
----------------------------------------
- After the user opens the client, the client requires the user to grant authorization
- User agrees to grant client authorization
- The client uses the authorization obtained in the previous step to apply for a token from the authentication server
- After the authentication server authenticates the client, it confirms that it is correct and agrees to issue the token
- The client uses the token to apply to the resource server to obtain resources
- The resource server confirms that the token is correct and agrees to open the resources to the client

Authorization code mode
----------------------------------------
Authorization code is the authorization mode with the most complete functions and the most stringent process. Its feature is to interact with the authentication server on the server through the client's backend server.

The process is:

- User accesses the client, the latter directs the former to the authentication server
- User chooses whether to grant client authorization
- Assuming that the user gives authorization, the authentication server directs the user to the "redirection URI" (redirection URI) specified by the client in advance, and attaches an authorization code.
- The client received the authorization code, attached the earlier "redirect URI", and applied for a token from the authentication server
- The authentication server checks the authorization code and redirection URI. After confirming that it is correct, it sends an access token and refresh token to the client.

In step A, the URI of the client applying for authentication includes the following parameters:

- response_type: indicates the authorization type, a required option, the value here is fixed as ``code``
- client_id: indicates the client's ID, a required option
- redirect_uri: represents a redirect URI, optional
- scope: indicates the scope of permissions for the application, optional
- state: indicates the current status of the client, and needs to be specified dynamically to prevent CSRF

For example:

::

GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com

In step C, the server responds to the client's URI, including the following parameters:

- code: indicates the authorization code, a required option. The validity period of this code should be very short and the client can only use the code once, otherwise it will be rejected by the authorized server. This code is one-to-one correspondence with the client ID and the redirect URI.
- state: If the client's request contains this parameter, the authentication server responds to the same parameter as when requested

For example:

::

HTTP/1.1 302 Found
Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz

In step D, the client applies for an HTTP request for the token from the authentication server, including the following parameters:

- grant_type: indicates the authorization mode used, a required option, the value here is fixed as ``authorization_code``
- code: indicates the authorization code obtained in the previous step, a required option
- redirect_uri: indicates a redirect URI, a required option, and must be consistent with the parameter value in step A.
- client_id: indicates client ID, a required option

For example:

::

POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb


In step E, the HTTP reply sent by the authentication server includes the following parameters:

- access_token: indicates access token, a required option
- token_type: Indicates the token type, the value is case-insensitive, a required option, which can be type ``bearer`` or type ``mac``
- expires_in: indicates expiration time, in seconds. If this parameter is omitted, the expiration time must be set in other ways
- refresh_token: indicates the update token, used to obtain the next access token, optional
- scope: indicates the permission scope. If it is consistent with the scope requested by the client, this item can be omitted

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
The simplicit grant type does not pass through the server of a third-party application, but directly applies for a token from the authentication server in the browser, skipping the step of authorization code, hence the name. All steps are done in the browser, the token is visible to the visitor, and the client does not require authentication.

The steps are:

- The client directs the user to the authentication server
- User decides whether to grant the client authorization
- Assuming that the user gives authorization, the authentication server directs the user to the redirect URI specified by the client and includes the access token in the Hash part of the URI
- The browser makes a request to the resource server, which does not include the hash value received in the previous step
- The resource server returns a web page with code that can get the token in the Hash value
- The browser executes the script obtained in the previous step and extracts the token
- The browser sends the token to the client

In step A, the HTTP request issued by the client contains the following parameters:

- response_type: indicates the authorization type, the value here is fixed to ``token``, a required option
- client_id: indicates the client's ID, a required option
- redirect_uri: represents a redirect URI, optional
- scope: indicates permission scope, optional
- state: indicates the current status of the client, and needs to be specified dynamically to prevent CSRF

For example:

::

GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com

In step C, the authentication server responds to the client's URI, including the following parameters:

- access_token: indicates access token, a required option
- token_type: Indicates the token type, the value is case-insensitive, a required option
- expires_in: indicates expiration time, in seconds. If this parameter is omitted, the expiration time must be set in other ways
- scope: indicates the permission scope. If it is consistent with the scope requested by the client, this item can be omitted
- state: If the client's request contains this parameter, the authentication server responds to the same parameter as when requested

For example:

::

HTTP/1.1 302 Found
Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA&state=xyz&token_type=example&expires_in=3600

In the above example, the authentication server uses the Location column of the HTTP header information to specify the URL redirected by the browser. Note that the Hash section of this URL contains the token.

According to the D step above, the browser will access the URL specified by Location in the next step, but the Hash part will not be sent. In the next E step, the code sent by the service provider's resource server will extract the token in the hash.

Password mode
----------------------------------------
In Resource Owner Password Credentials Grant, users provide their own username and password to the client. The client uses this information to ask for authorization from the "service provider".

In this mode, the user must give his/her password to the client, but the client must not store the password.

The steps are as follows:

- User provides the user name and password to the client
- The client sends the username and password to the authentication server and requests the token from the latter
- After the authentication server confirms that it is correct, provide the access token to the client

In step B, the HTTP request issued by the client contains the following parameters:

- grant_type: indicates the authorization type, the value here is fixed to ``password``, a required option
- username: indicates the username, a required option
- password: indicates the user's password, a required option
- scope: indicates permission scope, optional

For example:

::

POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=johndoe&password=A3ddj3w

In step C, the authentication server sends an access token to the client, for example:

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


Client Mode
----------------------------------------
Client Credentials Grant refers to the client authenticating to the server in its own name, rather than in the name of the user.

The steps are as follows:

- The client authenticates the authentication server and requires an access token
- After the authentication server confirms that it is correct, provide the access token to the client

In step A, the HTTP request issued by the client contains the following parameters:

- granttype: indicates the authorization type, the value here is fixed to ``clientcredentials``, a required option
- scope: indicates permission scope, optional

For example:

::

POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials

In step B, the authentication server sends an access token to the client, for example:

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
- `rfc6749 <Hr: //
- `Understanding OAuth <http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html>`_
- `OAuth 2.0 Vulnerabilities <https://ldapwiki.com/wiki/OAuth%202.0%20Vulnerabilities>`_
- `OAuth Community Site <https://oauth.net/>`_
- `Hidden OAuth attack vectors <https://portswigger.net/research/hidden-oauth-attack-vectors>`_
