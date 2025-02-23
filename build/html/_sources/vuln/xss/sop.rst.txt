Same Origin Policy
========================================

Introduction
----------------------------------------
Same-origin policies limit how resource interactions are conducted between different sources and are an important security mechanism for isolating potential malicious files.
Whether the same origin is determined by the URL. The URL consists of a protocol, domain name, port and path. If the protocol, domain name and port of the two URLs are the same, it means that they are the same origin.

Homogenic policy for file domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In previous browsers, the URIs of any two file domains were considered homologous. Any HTML file on the local disk can read any other file on the local disk.

Starting with Gecko 1.9, files use a more nuanced homologous strategy, and files can only read another file if the parent directory of the source file is the ancestor directory of the target file.

Same Origin Policy for Cookies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Cookies use different source definition methods. A page can set cookies for this domain and any parent domain as long as it is a parent domain and not a public suffix.

Regardless of which protocol (HTTP/HTTPS) or port number is used, the browser allows the given domain and any of its subdomains to access cookies. When setting cookies, you can use the ``domain`` / ``path`` / ``secure`` and ``http-only`` tags to limit their accessibility.

So the ``https://localhost:8080/` and ``http://localhost:8081/`` cookies are shared.

Flash/SilverLight Cross-domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Various plug-ins in the browser also have cross-domain requirements. Usually, by configuring crossdomain.xml on the server, setting up crossdomain access to this service.

The client will request this file. If it finds that its domain name is in the access list, it will initiate a real request, otherwise it will not send the request.

Changes to the source
----------------------------------------
Homology policies believe that domains and subdomains belong to different domains, such as ``child1.a.com`` vs. ``a.com`` / ``child1.a.com`` with ``child2.a.com`` / ``xxx.child1.a.com`` and ``child1.a.com`` have different sources.

For this case, you can set ``document.domain='a.com'` in two aspects to change its source to achieve communication between any of the above two pages.

In addition, because the browser saves the port number separately, this assignment will cause the port number to be ``null``.

Cross-original access
----------------------------------------
Homologous policies control interactions between different sources, which are usually divided into three categories:

+ Cross-origin writes are usually allowed
+ Links (links)
+ Redirect
+ Form Submission
+ Cross-origin embedding is usually allowed
+ Cross-origin reads are not usually allowed

Some examples of resources that may be embedded across origin are:

+ ``<script src="..."></script>`` Tags are embedded in cross-domain scripts. Syntax error messages can only be captured in homologous scripts.
+ ``<link rel="stylesheet" href="...">`` Tag embeds CSS. Due to the loose syntax rules of CSS, CSS needs a correct Content-Type message header to set up.
+ ``<img>`` / ``<video>`` / ``<audio>`` Embed multimedia resources.
+ ``<object>```````` and ``<embed>`` plugins.
+ ``@font-face`` font introduced. Some browsers allow cross-origin fonts, while some require same-origin fonts.
+ ``<frame>`` and ``<iframe>`` any resource loaded. Sites can use X-Frame-Options message headers to block this form of cross-domain interaction.

JSONP Cross-domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
JSONP uses the cross-domain capability of the ``<script>`` tag to achieve cross-domain data access, requesting that the dynamically generated JavaScript script also bring a callback function name as a parameter.

After the server receives the request, it dynamically generates the script to generate data, and calls the callback function with the generated data as parameters in the code.

JSONP also has some security problems, such as when returning directly without verification of incoming/return parameters, it will cause XSS problems. Data leakage may occur when data is given without Referer or Token verification.

In addition, JSONP can legally make some function calls outside the design without setting a whitelist of callback functions to introduce problems. This kind of attack is also called a SOME attack.

Cross-origin script API access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Javascript APIs, such as ``iframe.contentWindow`, ``window.parent`, ``window.open` and ``window.opener` allow documents to be referenced. When the sources of the two documents are different, these references will add restrictions on access to the ``window`` and ``location`` objects.

``window`` methods that allow cross-origin access are

- window.blur
- window.close
- window.focus
- window.postMessage

``window`` properties that allow cross-origin access are

- window.closed
- window.frames
- window.length
- window.location
- window.opener
- window.parent
- window.self
- window.top
- window.window

Among them, ``window.location`` allows reading/writing, and other attributes only allow reading.

Cross-origin data storage access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data stored in the browser, such as ``localStorage`` and ``IndexedDB``, are split by source. Each source has its own separate storage space, and Javascript scripts in one source cannot read and write data belonging to other sources.

CORS
----------------------------------------
CORS is a W3C standard, and its full name is Cross-origin resource sharing. Through this standard, browsers can be allowed to read cross-domain resources.

Common request headers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Origin
- The source site URI of the pre-check request or actual request, the browser request will send this field by default
- ``Origin: <origin>``
- Access-Control-Request-Method
- Declare the method to use the request
- ``Access-Control-Request-Method: <method>``
- Access-Control-Request-Headers
- Declare the header field used by the request
- ``Access-Control-Request-Headers: <field-name>[, <field-name>]*``

Common return to the head
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Access-Control-Allow-Origin
- Declare the source outdated URI that is allowed to access
- Wildcard characters ``*`````` for requests carrying credentials
- ``Access-Control-Allow-Origin: <origin> | *``
- Access-Control-Expose-Headers
- Declares that the exposed heads are allowed
- e.g. ``Access-Control-Expose-Headers: X-My-Custom-Header, X-Another-Custom-Header``
- Access-Control-Max-Age
- Statement of Cache Time
- ``Access-Control-Max-Age: <delta-seconds>``
- Access-Control-Allow-Credentials
- Declare whether to allow bringing in in the request
- ``Access-Control-Allow-Credentials: true``
- Access-Control-Allow-Methods
- Declare the allowed access method
- ``Access-Control-Allow-Methods: <method>[, <method>]*``
- Access-Control-Allow-Headers
- Declare allowed headers
- ``Access-Control-Allow-Headers: <field-name>[, <field-name>]*``

Defense advice
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Do not enable CORS unless necessary
- Define a detailed whitelist, do not use wildcards, only configure the required headers
- Configuration ``Vary: Origin`` header
- Do not use ``Access-Control-Allow-Credentials`` unless necessary
- Limit cache time

Block cross-origin access
----------------------------------------
Block cross-domain write operations and can detect ``CSRF token`` in a request, which is called the Cross-Site Request Forgery (CSRF) tag.

Block cross-site reading of resources, because embedded resources usually expose information, and it is necessary to ensure that resources are not embedded. However, in most cases, the browser will not comply with the ``Content-Type` message header. For example, if you specify the ``<script>`` tag in an HTML document, the browser will try to parse the HTML into JavaScript.
