取证
================================

在运维时，从日志中获取信息是十分有必要的
可以发现成功或未成功的入侵行为

一个是从ua入手，一些工具都会有比较明显的ua，比如下面这些常用的漏扫

awvs/appscan/netsparker/burpsuite/webcuriser/vega/owasp zap/nikto/w3af/nessus/openvas

另外，可以针对每种攻击进行关键字匹配
比如select/alert/eval等

还有连续的404或者500就可能是攻击者在进行尝试

参考链接
---------------------------------------------
- `取证入门 web篇 <http://www.freebuf.com/column/147929.html>`_