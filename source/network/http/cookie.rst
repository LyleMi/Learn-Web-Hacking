Cookie
========================================

Introduction
----------------------------------------
Cookies (plural form cookies), type "small text file", refer to data stored on the user's local terminal in order to identify the user's identity.

property
----------------------------------------

name
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The name of the cookie.

value
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The value of the cookie.

expires
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When the Expires property defaults, it means it is a session cookie, which is invalid when the user closes the browser.

max-age
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
max-age can be positive, negative, and 0. If the max-age attribute is positive, the browser will persist it. When the max-age attribute is negative, it means that the cookie is just a session cookie. When max-age is 0, this cookie is deleted immediately. Under the conditions where both Expires and max-age exist, max-age has higher priority.

domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Specify the domain name of the cookie, the default is the current domain name. When setting the domain, it can be set to itself and its parent domain. The child domain can access the cookies of the parent domain, otherwise it cannot.

path
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Specify a URL path that must appear in the path of the resource to be requested before the corresponding cookie can be sent.

secure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Transfers only over HTTPS.

httponly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Restriction cookies to be read only during HTTP transmission, and to a certain extent, they are protected from XSS attacks.

The sames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SameSite supports three values: Strict/Lax/None. Strict is the strictest, completely prohibiting third-party cookies. Cookies will not be sent under any circumstances when cross-sites. Lax allows some third parties to request cookies, mainly in three situations: link, preload, and GET forms. When the SameSite property of a cookie is None, and Secure is set, cookies will be sent regardless of whether they are cross-site or not.
