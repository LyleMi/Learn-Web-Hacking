Cookie
========================================

Introduction
----------------------------------------
Cookies (plural Cookies), a type of "small text file", refer to the data that some websites store on the user's local terminal in order to identify the user's identity.

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
When the Expires attribute is defaulted, it means that it is a session cookie and expires when the user closes the browser.

max-age
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
max-age can be positive, negative, or 0. If the max-age attribute is a positive number, the browser will persist it. When the max-age attribute is a negative number, it means that the cookie is only a session cookie. When max-age is 0, the cookie will be deleted immediately. When both Expires and max-age exist, max-age has higher priority.

domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Specify the domain name of the cookie. The default is the current domain name. When setting the domain, it can be set to itself and its parent domain. The child domain can access the cookies of the parent domain, but not vice versa.

path
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Specify a URL path, which must appear in the path of the resource to be requested before the corresponding cookie can be sent.

secure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Can only be transferred via HTTPS.

httponly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Limit cookies to be read only during HTTP transmission, preventing XSS attacks to a certain extent.

SameSite
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SameSite supports three values: Strict / Lax / None. Strict is the most stringent and completely prohibits third-party cookies. When cross-site, cookies will not be sent under any circumstances. Lax allows some third-party requests to carry cookies, mainly for links, preloading, and GET forms. When the Cookie's SameSite attribute is None and Secure is set, the Cookie will be sent regardless of whether it is cross-site.
