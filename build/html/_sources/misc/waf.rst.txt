WAF
========================================

Introduction
----------------------------------------

concept
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WAF (Web Application Firewall) is a product that specifically provides reinforcement for web applications by executing a series of security policies for HTTP/HTTPS.

On the market, there are WAFs with various prices and various features and options. To a certain extent, WAF can provide security for web applications, but cannot guarantee complete security.

Common features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Detect exception protocol, reject requests that do not comply with HTTP standards
- Session protection for state management
- Cookies protection
- Information leakage protection
- DDoS protection
- Disable certain IP access
- Suspicious IP check
- Secure HTTP header management
- X-XSS-Protection
- X-Frame-Options
- Mechanism detection
- CSRF token
- HSTS

Arrangement location
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
According to the layout position, WAF can be divided into cloud WAF, host protection software and hardware protection. Cloud WAF is arranged on the cloud, and requests are first passed through the cloud server and then flow to the host. The host protection software requires the host to pre-install corresponding software, such as mod_security, ngx-lua-waf, etc., to protect the host. Hardware protection refers to the cleaning and intercepting of the equipment when traffic flows to the host.

Protection method
----------------------------------------
Common methods of WAF include keyword detection, regular expression detection, syntax analysis, behavioral analysis, reputation analysis, machine learning, etc.

Regular-based protection is the most common way to protect. Developers use some set regular rules to detect whether the payload is aggressive. Regular protection is relatively simple, so there are some disadvantages. For example, it can only be applied to single requests, and regularity is difficult to apply to some complex protocols.

Syntax-based analysis is faster and more accurate than regularity. This analysis parses the load into symbol groups according to the syntax, and then looks for dangerous keywords in the symbol groups. This method has better effect on some load variations, but also has higher requirements for parsers.

Behavior-based analysis focuses on a wider range, such as attacker's port scanning behavior, directory blasting, parameter testing, or some other automation or attack modes will be taken into consideration.

Reputation-based analysis can filter out some suspicious sources, such as commonly used VPNs, anonymous proxy, Tor nodes, and botnet nodes' IPs.

WAF based on machine learning involves a very wide range, and the effects are more diverse due to specific implementations and scenarios.

In addition to being classified according to specific methods, it can also be classified according to the use of whitelists and blacklists. Whitelist-based WAF is suitable for stable web applications, while blacklist-based is suitable for handling known issues.

Scanner Defense
----------------------------------------
- User-Agent-based identification
- Based on attack payload identification
- Verification code

WAF fingerprint
----------------------------------------
- Additional Cookies
- Additional Header
- Return content when request is rejected
- Return response code when request is rejected
- IP

Bypass method
----------------------------------------

Architecture-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The site is after WAF, but the site can be directly connected
- The site is in a cloud server, and there is no WAF for the same network server

Resource-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Use high-consuming loads to exhaust WAF's computing resources
- Provides a large number of invalid parameters

Analytical-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Character set parsing differently
- Incomplete protocol coverage
- POST's JSON parameter / ``form-data`` / ``multipart/form-data``
- Protocol parsing is incorrect
- There are partial inconsistencies between the site and WAF for https
- WAF parsing and web service parsing are inconsistent
- Some ASP+IIS convert characters in the ``%u0065`` format
- Apache will parse the deformed method
- The same parameter appears multiple times, and the positions are taken differently
- HTTP Parameter Pollution (HPP)
- HTTP Parameter Fragmentation (HPF)

Rule-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Equivalent substitution
-Case transformation
- ``select`` => ``sEleCt``
- ``<sCrIpt>alert(1)</script>``
- Character encoding
- URL encoding
- Hexadecimal encoding
- Unicode analysis
- Base64
- HTML
- JSFuck
- Other encoding formats
- Equivalent function
- Equivalent variables
- Keyword splitting
- String operation
- Character interference
- Empty characters
- NULL (\x00)
- Spaces
- Enter (\x0d)
- Line break (\x0a)
- Vertical Tabulation (\x0b)
- Horizontal Tabulation (\x09)
- Page Change (\x0c)
- Comments
- Special symbols
- Comment characters
- Quotation marks (back quotes, single quotes, double quotes)
-Use the features of the service itself
- Replace suspicious keywords with empty
- ``selselectect`` => ``select``
- Rare features are not in the rule list

Reference link
----------------------------------------
- `Four levels of WAF offensive and defense research Bypass WAF <https://www.weibo.com/ttarticle/p/show?id=2309404007261092631700&sudaref=www.google.com.hk&display=0&retcode=6102>`_
- `My Way of Way SQL Injection <https://xz.aliyun.com/t/368>`_
- `WAF through the eyes of hackers <https://habr.com/en/company/dsec/blog/454592/>`_
