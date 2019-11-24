# Web安全学习笔记

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

### 序言
---

在学习Web安全的过程中，深切地感受到相关的知识浩如烟海，而且很大一部分知识点都相对零散，如果没有相对清晰的脉络作为参考，会给学习带来一些不必要的负担。于是在这之后尝试把一些知识、想法整理记录下来，最后形成了这份笔记。希望这份笔记能够为正在入门的网络安全爱好者提供一定的帮助。

笔记内容总体分为四个部分。第一部分围绕Web相关的基础知识如计算机网络、域名系统、HTTP协议等做了一定的说明，这些知识是进行Web安全学习的基础。第二部分按照常见的渗透测试的顺序，对信息收集、常见的Web漏洞、常见语言与框架、内网渗透的技巧等进行了简单的讲述，开始渗透测试之后通常会接触到这部分内容。第三部分回到防御的视角，从安全团队的建设、威胁情报与风控等较大的视角做了描述，也对蜜罐、溯源等较为细节的内容作了说明。最后一部分推荐了一些工具与资源列表，也把一些没有分类的内容暂时归档到这一部分。

笔者所学浅薄、精力有限，在整理笔记的过程中难免存在一些错误或是不完整的部分，正在逐渐修正和补充。如果存在错误，欢迎各位读者以[Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new)或者[PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls)的方式批评指正，感激不尽。

在编写笔记的过程中参考、摘抄了很多资料，都在文末留下了相应的链接，十分感谢文章作者的分享。其中笔记的在线版本可以点击[这里](https://websec.readthedocs.io)查看。

### 笔记大纲
---

1. 基础知识
    - Web技术演化
    - 计算机网络
    - 域名系统
    - HTTP标准
    - 代码审计
    - WAF
2. 信息收集
    - 域名信息
    - 站点信息
    - 端口信息
3. 常见漏洞
    - SQL注入
    - XSS
    - CSRF
    - SSRF
    - 命令注入
    - 文件读取
    - 文件上传
    - 文件包含
    - XXE
    - 模版注入
    - Xpath注入
    - 逻辑漏洞 / 业务漏洞
    - 配置安全
    - 中间件
    - Web Cache欺骗攻击
4. 语言与框架
    - PHP
    - Python
    - Java
    - JavaScript
    - Ruby
    - ASP
5. 内网渗透
    - Windows信息收集
    - Windows持久化
    - Linux信息收集
    - 痕迹清理
6. 防御技术
    - 团队建设
    - 安全开发
    - 威胁情报
    - 风险控制
    - 加固检查
    - 蜜罐技术
    - 入侵检测
    - 应急响应
    - 溯源分析
7. 认证机制
    - OAuth
    - JWT
    - Kerberos
    - SAML
8. 工具与资源
    - 推荐资源
    - 相关论文
    - 信息收集
    - 社会工程学
    - Fuzz
    - 漏洞利用
    - 持久化
    - 防御
    - 运维
9. 手册速查
    - 爆破工具
    - 下载工具
    - 流量相关
    - 嗅探工具
    - SQLMap
9. 其他
    - Unicode
    - 拒绝服务攻击
    - Docker

### 本地编译
---

```bash
git clone https://github.com/LyleMi/Learn-Web-Hacking.git
cd Learn-Web-Hacking
pip install sphinx sphinx-rtd-theme
make html
```

### Contribution
---

如果有任何的问题、意见或者建议欢迎以Issue或PR的形式提出，不胜感激。

感谢所有的[贡献者](https://github.com/LyleMi/Learn-Web-Hacking/graphs/contributors)。

### License
---

项目以CC0 1.0许可证发布，可以点击[这里](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/LICENSE)浏览全文。

### 注
---

该笔记仅供学习和交流使用，请读者遵守《[中华人民共和国网络安全法](http://www.npc.gov.cn/npc/xinwen/2016-11/07/content_2001605.htm)》，勿进行非授权的测试。
