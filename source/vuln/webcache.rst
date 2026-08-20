Web Cache spoofing attack
================================

Introduction
--------------------------------
Websites usually implement web caching functions through CDN, load balancer, or reverse proxy. Reduce server response latency by caching frequently accessed files.

For example, the website ``http://www.example.com`` is configured with a reverse proxy. For pages that contain users' personal information, such as ``http://www.example.com/home.php``, since the content returned by each user is different, such pages are usually dynamically generated and will not be cached in the cache server. Usually, cached files are mainly publicly accessible static files, such as css files, js files, txt files, pictures, etc. Additionally, many best practices articles recommend caching publicly accessible static files and ignoring HTTP cache headers.

Web cache attacks are similar to RPO relative path rewrite attacks, both of which rely on the way the browser and server parse URLs. When accessing a non-existent URL, such as ``http://www.example.com/home.php/non-existent.css``, the browser sends a get request. Depending on the technology and configuration used, the server returns the content of the page ``http://www.example.com/home.php``. At the same time, the URL address is still ``http://www.example.com/home.php/non-existent.css``, and the content of the http header is also the same as direct access. ``http://www.example.com/home.php`` is the same, as are the caching header and content-type (here, text/html).

Vulnerability causes
--------------------------------
What happens when ``http://www.example.com/home.php/no-existent.css`` is accessed when the proxy server is set up to cache static files and ignores the caching header for such files? The entire response process is as follows:

1. The browser requests ``http://www.example.com/home.php/no-existent.css``;
2. The server returns the content of ``http://www.example.com/home.php`` (usually this page will not be cached);
3. The response passes through the proxy server;
4. The agent recognizes that the file has a css suffix;
5. In the cache directory, the proxy server creates the directory ``home.php`` and saves the returned content as ``non-existent.css``.

exploit
--------------------------------
The attacker deceives users to visit ``http://www.example.com/home.php/logo.png?www.myhack58.com``, causing the page containing the user's personal information to be cached and thus publicly accessible. In more serious cases, if the returned content contains session identification, answers to security questions, or CSRF tokens. An attacker can then obtain this information because typically most static resources on a website are publicly accessible.

Conditions for the vulnerability to exist
--------------------------------
For a vulnerability to exist, at least the following two conditions must be met:

1. The web cache function saves according to the extension and ignores the cache header;
2. When accessing a non-existent page such as ``http://www.example.com/home.php/non-existent.css``, the content of ``home.php`` will be returned.

Vulnerability defense
--------------------------------
Defense measures mainly include three points:

1. Set up a caching mechanism to only cache files allowed by the http caching header, which can fundamentally eliminate this problem;
2. If the cache component provides options, set it to cache based on content-type;
3. When accessing non-existent pages such as ``http://www.example.com/home.php/non-existent.css``, the content of ``home.php`` will not be returned, but 404 or 302 will be returned.

Web Cache spoofing attack example
--------------------------------
Paypal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Before Paypal is repaired, the information that can be obtained through this attack includes: user name, account amount, last 4 digits of credit card, transaction data, email address and other information.
Some of the pages affected by this attack include:

- ``https://www.paypal.com/myaccount/home/attack.css``
- ``https://www.paypal.com/myaccount/settings/notifications/attack.css``
- ``https://history.paypal.com/cgi-bin/webscr/attack.css?cmd=_history-details`` 。

Reference link
--------------------------------
- `practical web cache poisoning <https://portswigger.net/blog/practical-web-cache-poisoning>`_
- `End-Users Get Maneuvered: Empirical Analysis of Redirection Hijacking in Content Delivery Networks <https://www.usenix.org/conference/usenixsecurity18/presentation/hao>`_
