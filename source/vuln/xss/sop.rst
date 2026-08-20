Same origin policy
========================================

Introduction
----------------------------------------
The same-origin policy restricts how resources interact between different sources and is an important security mechanism for isolating potentially malicious files.
Whether they have the same origin is determined by the URL, which consists of protocol, domain name, port and path. If the protocol, domain name and port of two URLs are the same, it means they have the same origin.

Same-origin policy for file domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In previous browsers, any two file domain URIs were considered to have the same origin. Any HTML file on the local disk can read any other file on the local disk.

Starting with Gecko 1.9, files use a more granular same-origin policy, and a file can only read another file if the parent directory of the source file is the ancestor directory of the target file.

Same origin policy for cookies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Cookies use different source definitions. A page can set cookies for this domain and any parent domain, as long as the parent domain is not a public suffix.

Regardless of the protocol (HTTP/HTTPS) or port number used, the browser allows a given domain and any of its subdomains to access the cookie. When setting a cookie, you can limit its accessibility using the ``domain`` / ``path`` / ``secure`` and ``http-only`` tags.

So the cookies of ``https://localhost:8080/`` and ``http://localhost:8081/`` are shared.

Flash/SilverLight cross domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are also cross-domain requirements for various browser plug-ins. Usually, crossdomain.xml is configured on the server to set which domain names the service allows for cross-domain access.

The client will request this file. If it finds that its domain name is in the access list, it will initiate a real request, otherwise it will not send the request.

Source changes
----------------------------------------
The same-origin policy considers that domains and subdomains belong to different domains. For example, ``child1.a.com`` and ``a.com`` / ``child1.a.com`` and ``child2.a.com`` / ``xxx.child1.a.com`` and ``child1.a.com`` are not from the same source.

In this case, you can set ``document.domain='a.com'`` on both sides to change their sources to achieve communication between any two of the above pages.

In addition, because the browser saves the port number separately, this assignment will cause the port number to be rewritten as ``null``.

Cross-origin access
----------------------------------------
The same-origin policy controls interactions between different origins, and these interactions are usually divided into three categories:

+ Usually allows cross-origin writes (Cross-origin writes)
    + links
    + redirect
    + form submission
+ Usually allows cross-origin embedding
+ Cross-origin reads are generally not allowed

Some examples of resources that may be embedded across origins are:

+ ``<script src="..."></script>`` tag embeds cross-domain scripts. Syntax error messages can only be caught in originating scripts.
+ ``<link rel="stylesheet" href="...">`` tag embedded in CSS. Due to the loose syntax rules of CSS, cross-domain CSS requires a properly set Content-Type header.
+ ``<img>`` / ``<video>`` / ``<audio>`` Embed multimedia resources.
+ Plugins for ``<object>`` ``<embed>`` and ``<applet>``.
+ Font introduced by ``@font-face``. Some browsers allow cross-origin fonts, and some require same-origin fonts.
+ Any resources loaded by ``<frame>`` and ``<iframe>``. Sites can use the X-Frame-Options header to prevent this form of cross-domain interaction.

JSONP cross domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
JSONP uses the cross-domain capability of the ``<script>`` tag to achieve cross-domain data access, requesting a dynamically generated JavaScript script with a callback function name as a parameter.

After the server receives the request, it dynamically generates a script to generate data, and calls the callback function in the code with the generated data as a parameter.

JSONP also has some security issues. For example, when the incoming/returning parameters are directly returned without verification, XSS problems will occur. When data is given without referer or token verification, data leakage may occur.

In addition, JSONP can legally make some undesigned function calls without setting a whitelist for the callback function, causing problems. This attack is also known as SOME attack.

Cross-origin scripting API access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Javascript APIs such as ``iframe.contentWindow``, ``window.parent``, ``window.open`` and ``window.opener`` allow documents to reference each other. These referencing methods will add restrictions on access to the ``window`` and ``location`` objects when the sources of the two documents are different.

``window`` methods that allow cross-origin access include

- window.blur
- window.close
- window.focus
- window.postMessage

The attributes of ``window`` that allow cross-origin access are

- window.closed
- window.frames
- window.length
- window.location
- window.opener
- window.parent
- window.self
- window.top
- window.window

Among them, ``window.location`` allows reading/writing, and other properties only allow reading.

Cross-origin data storage access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data stored in the browser, such as ``localStorage`` and ``IndexedDB``, is split by source. Each source has its own separate storage space, and Javascript scripts in one source cannot read or write data belonging to other sources.

CORS
----------------------------------------
CORS is a W3C standard, whose full name is Cross-origin resource sharing. Through this standard, browsers can be allowed to read cross-domain resources.

Common request headers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Origin
    - The origin URI of the preflight request or actual request, this field will be sent by default in browser requests
    - ``Origin: <origin>``
- Access-Control-Request-Method
    - Declare the method used by the request
    - ``Access-Control-Request-Method: <method>``
- Access-Control-Request-Headers
    - Declare the header fields used in the request
    - ``Access-Control-Request-Headers: <field-name>[, <field-name>]*``

Common return headers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Access-Control-Allow-Origin
    - Declare the source foreign domain URI that is allowed to access
    - The wildcard character ``*`` cannot be used for requests carrying identity credentials.
    - ``Access-Control-Allow-Origin: <origin> | *``
- Access-Control-Expose-Headers
    - Declare allowed exposed headers
    - e.g. ``Access-Control-Expose-Headers: X-My-Custom-Header, X-Another-Custom-Header``
- Access-Control-Max-Age
    - Declare cache time
    - ``Access-Control-Max-Age: <delta-seconds>``
- Access-Control-Allow-Credentials
    - Declare whether to allow in requests
    - ``Access-Control-Allow-Credentials: true``
- Access-Control-Allow-Methods
    - Declare allowed access methods
    - ``Access-Control-Allow-Methods: <method>[, <method>]*``
- Access-Control-Allow-Headers
    - Declare allowed headers
    - ``Access-Control-Allow-Headers: <field-name>[, <field-name>]*``

Defense Advice
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Do not enable CORS unless necessary
- Define detailed whitelist, do not use wildcards, configure only required headers
- Configure the ``Vary: Origin`` header
- Do not use ``Access-Control-Allow-Credentials`` unless necessary
- Limit cache time

Block cross-origin access
----------------------------------------
To prevent cross-domain write operations, you can detect the ``CSRF token`` in the request. This tag is called the Cross-Site Request Forgery (CSRF) tag.

Prevent cross-site reading of resources, because embedding resources usually exposes information, and it is necessary to ensure that the resources are not embeddable. But in most cases browsers do not respect the ``Content-Type`` header. For example, if you specify the ``<script>`` tag in an HTML document, the browser will attempt to parse the HTML into JavaScript.
