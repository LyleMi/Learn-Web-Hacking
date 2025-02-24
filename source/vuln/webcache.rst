Web Cache spoofing attack
================================

Introduction
--------------------------------
Websites usually implement web caching functions through CDNs, load balancers, or reverse proxy. Reduce server response latency by cacheing frequently accessed files.

For example, the website ``htttp://www.example.com` is configured with a reverse proxy. For pages that contain user personal information, such as ``http://www.example.com/home.php``, since the content returned by each user is different, such pages are usually generated dynamically and are not It will be cached in the cache server. Usually, the cache is mainly publicly accessible static files, such as css files, js files, txt files, pictures, etc. In addition, many best practice articles also recommend caching of static files that can be accessed publicly and ignore the HTTP cache header.

Web cache attacks are similar to RPO relative path rewriting attacks, and they all rely on the browser and server to parse URLs. When accessing a non-existent URL, such as ``http://www.example.com/home.php/non-existent.css``, the browser sends a get request, depending on the technology and configuration used, and the server returns The content of the page ``http://www.example.com/home.php``, and the URL address is still ``http://www.example.com/home.php/non-existent.css``. The content of the http header is also the same as the direct access to ``http://www.example.com/home.php``, and the cacheing header and content-type (here is text/html).

Causes of vulnerabilities
--------------------------------
What happens when the proxy server is set to cache static files and ignores the cache header for such files? What happens when you access ``http://www.example.com/home.php/no-existent.css``? The entire response process is as follows:

1. Browser request ``http://www.example.com/home.php/no-existent.css`` ;
2. The server returns the content of ``http://www.example.com/home.php`` (usually, the page will not be cached);
3. Response through the proxy server;
4. The proxy recognizes that the file has a css suffix;
5. In the cache directory, the proxy server creates the directory ``home.php`` and saves the returned content as ``non-existent.css`.

Vulnerability exploitation
--------------------------------
The attacker deceived users to access ``http://www.example.com/home.php/logo.png?www.myhack58.com`, resulting in the page containing the user's personal information being cached and can be accessed publicly. In more serious cases, if the returned content contains the session identifier, answers to security questions, or csrf token. This way the attacker can then obtain this information, because generally most static resources on the website are publicly accessible.

Conditions for the existence of a vulnerability
--------------------------------
To exist, at least the following two conditions need to be met:

1. The web cache function is saved according to the extension and ignores the caching header;
2. When accessing a page that does not exist such as ``http://www.example.com/home.php/non-existent.css``, the content of ``home.php`` will be returned.

Vulnerability Defense
--------------------------------
The defense measures mainly include 3 points:

1. Set up a caching mechanism to only cache files allowed by the http caching header, which can fundamentally eliminate this problem;
2. If the cache component provides options, set to cache according to content-type;
3. Visit ``http://www.example.com/home.php/non-existent.css``, which does not exist in this type of page, does not return the content of ``home.php``, but returns 404 or 302.

Web Cache spoofing attack example
--------------------------------
Paypal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Before Paypal was repaired, the information that can be obtained through this attack includes: user name, account amount, last 4 digits of credit card, transaction data, email address and other information.
Some of the pages under this attack include:

- ``https://www.paypal.com/myaccount/home/attack.css``
- ``https://www.paypal.com/myaccount/settings/notifications/attack.css``
- ``https://history.paypal.com/cgi-bin/webscr/attack.css?cmd=_history-details`` 。

Reference link
--------------------------------
- `practical web cache poisoning <https://portswigger.net/blog/practical-web-cache-poisoning>`_
- `End-Users Get Maneuvered: Empirical Analysis of Redirection Hijacking in Content Delivery Networks <https://www.usenix.org/conference/usenixsecurity18/presentation/hao>`_
