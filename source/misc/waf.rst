WAF
========================================

Introduction
----------------------------------------

concept
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WAF (Web Application Firewall, Web Application Firewall) is a product that specifically provides reinforcement for Web applications by executing a series of security policies for HTTP/HTTPS.

In the market, there are WAFs with various features and options at various prices. To a certain extent, WAF can provide security for web applications, but it cannot guarantee complete security.

Common functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Detect abnormal protocols and reject requests that do not comply with HTTP standards
- Session protection for state management
- Cookie protection
- Information leakage protection
- DDoS protection
-Ban access to certain IPs
- Suspicious IP check
- Secure HTTP header management
    - X-XSS-Protection
    - X-Frame-Options
- Mechanism detection
    - CSRF token
    - HSTS

layout location
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
According to the deployment location, WAF can be divided into cloud WAF, host protection software and hardware protection. Cloud WAF is deployed on the cloud, and requests first pass through the cloud server and then flow to the host. Host protection software requires the host to pre-install corresponding software, such as mod_security, ngx-lua-waf, etc., to protect the host. Hardware protection means that when traffic flows to the host, it is first cleaned and intercepted by the device.

Protection method
----------------------------------------
Commonly used methods for WAF include keyword detection, regular expression detection, syntax analysis, behavior analysis, reputation analysis, machine learning, etc.

Regularity-based protection is the most common protection method. Developers use some set regular rules to detect whether the payload is offensive. Regularity-based protection is simpler and therefore has some disadvantages. For example, it can only be applied to a single request, and regularity is difficult to apply to some complex protocols.

Syntax-based analysis is faster and more accurate than regular expressions. This analysis parses the payload into symbol groups according to the grammar, and then looks for dangerous keywords in the symbol groups. This method has better effects on some payload variations, but also has higher requirements on the parser.

Behavior-based analysis looks at a wider scope, such as the attacker's port scanning behavior, directory blasting, parameter testing or some other automation or attack patterns will be taken into consideration.

Reputation-based analysis can better filter out some suspicious sources, such as commonly used VPNs, anonymous proxies, Tor nodes, botnet node IPs, etc.

WAF based on machine learning covers a very wide range, and the effects are more diverse depending on the specific implementation and scenarios.

In addition to dividing by specific methods, they can also be classified according to the use of whitelists and blacklists. Whitelist-based WAF is suitable for stable web applications, while blacklist-based WAF is suitable for dealing with known issues.

Scanner Defense
----------------------------------------
- Based on User-Agent identification
- Identification based on attack payload
- Verification code

WAF fingerprint
----------------------------------------
- Additional cookies
- Additional Header
-Return content when the request is rejected
-Response code when the request is rejected
- IP

Bypass
----------------------------------------

Architecture-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The site is behind the WAF, but the site can be directly connected
- The site is in a cloud server, and there is no WAF for servers in the same network segment.

Resource-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Use expensive loads to exhaust WAF’s computing resources
- Provide a large number of invalid parameters

Parsing-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-Character set parsing is different
-Incomplete agreement coverage
    - POST JSON parameters / ``form-data`` / ``multipart/form-data``
- Incorrect protocol parsing
- There are some inconsistencies between the site and WAF regarding https
- WAF parsing is inconsistent with Web service parsing
    - Some ASP+IIS will convert characters in ``%u0065`` format
    - Apache will parse malformed Method
    - The same parameter appears multiple times in different positions.
    - HTTP Parameter Pollution (HPP)
    - HTTP Parameter Fragmentation (HPF)

Rule-based bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Equivalent replacement
    - Case conversion
        - ``select`` => ``sEleCt``
        - ``<sCrIpt>alert(1)</script>``
    - character encoding
        - URL encoding
        - Hexadecimal encoding
        -Unicode parsing
        - Base64
        - HTML
        - JSFuck
        - Other encoding formats
    - Equivalent function
    - Equivalent variables
    - Keyword splitting
    - String operations
- character interference
    - null character
        - NULL (\x00)
        - space
        - Enter (\x0d)
        - newline (\x0a)
        - Vertical tab (\x0b)
        - Horizontal tab (\x09)
        - Page feed (\x0c)
    - Comments
- special symbols
    - comment character
    - Quotes (backticks, single quotes, double quotes)
- Take advantage of the features of the service itself
    - Replace suspicious keywords with empty
        - ``selselectect`` => ``select``
- Rare features are not in the rule list

Reference link
----------------------------------------
- `Four levels of WAF attack and defense research Bypass WAF <https://www.weibo.com/ttarticle/p/show?id=2309404007261092631700&sudaref=www.google.com.hk&display=0&retcode=6102>`_
- `My WafBypass Way SQL Injection <https://xz.aliyun.com/t/368>`_
- `WAF through the eyes of hackers <https://habr.com/en/company/dsec/blog/454592/>`_
