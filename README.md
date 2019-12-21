# Web安全学习笔记

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

### 序言
---

在学习Web安全的过程中，深切地感受到相关的知识浩如烟海，而且很大一部分知识点都相对零散，如果没有相对清晰的脉络作为参考，会给学习带来一些不必要的负担。于是在这之后尝试把一些知识、想法整理记录下来，最后形成了这份笔记。希望这份笔记能够为正在入门的网络安全爱好者提供一定的帮助。

笔记内容总体分为四个部分。第一部分围绕一些基础知识和技巧进行了一定的说明，主要Web技术的发展与演化、安全领域的基本常识、计算机网络的基础知识等，这些知识是进行Web安全学习的基础。第二部分按照常见的渗透测试的顺序，对信息收集、常见的Web漏洞、常见语言与框架、内网渗透的技巧等进行了简单的讲述，开始学习渗透测试之后通常会接触到这部分内容。第三部分回到防御的视角，从安全团队的建设、威胁情报与风控等较大的视角做了描述，也对蜜罐、溯源等较为细节的内容作了说明。最后一部分推荐了一些工具与资源列表，也把一些没有分类的内容暂时归档到这一部分。

笔者所学浅薄、精力有限，在整理笔记的过程中难免存在一些错误或是不完整的部分，正在逐渐修正和补充。如果存在错误，欢迎各位读者以[Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new)或者[PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls)的方式批评指正，感激不尽。

在编写笔记的过程中参考、摘抄了很多资料，都在文末留下了相应的链接，十分感谢文章作者的分享。其中笔记的在线版本可以点击[这里](https://websec.readthedocs.io)查看。

### 笔记大纲
---

1. 序章
    1.1. Web技术演化
    1.2. Web攻防技术演化
    1.3. 安全观
2. 计算机网络与协议
    2.1. 网络基础
    2.2. UDP协议
    2.3. 路由算法
    2.4. 域名系统
    2.5. HTTP标准
3. 信息收集
    3.1. 域名信息
    3.2. 端口信息
    3.3. 站点信息
    3.4. 搜索引擎利用
    3.5. 社会工程学
    3.6. 参考链接
4. 常见漏洞
    4.1. SQL注入
    4.2. XSS
    4.3. CSRF
    4.4. SSRF
    4.5. 命令注入
    4.6. 目录穿越
    4.7. 文件读取
    4.8. 文件上传
    4.9. 文件包含
    4.10. XXE
    4.11. 模版注入
    4.12. Xpath注入
    4.13. 逻辑漏洞 / 业务漏洞
    4.14. 配置安全
    4.15. 中间件
    4.16. Web Cache欺骗攻击
    4.17. HTTP 请求走私
5. 语言与框架
    5.1. PHP
    5.2. Python
    5.3. Java
    5.4. JavaScript
    5.5. Golang
    5.6. Ruby
    5.7. ASP
6. 内网渗透
    6.1. 信息收集 - Windows
    6.2. 持久化 - Windows
    6.3. 信息收集 - Linux
    6.4. 持久化 - Linux
    6.5. 痕迹清理
    6.6. 综合技巧
    6.7. 参考链接
7. 防御技术
    7.1. 团队建设
    7.2. 安全开发
    7.3. 威胁情报
    7.4. ​​ATT&CK
    7.5. 风险控制
    7.6. 加固检查
    7.7. 防御框架
    7.8. 蜜罐技术
    7.9. 入侵检测
    7.10. 应急响应
    7.11. 溯源分析
8. 认证机制
    8.1. OAuth
    8.2. JWT
    8.3. Kerberos
    8.4. SAML
9. 工具与资源
    9.1. 推荐资源
    9.2. 相关论文
    9.3. 信息收集
    9.4. 社会工程学
    9.5. 模糊测试
    9.6. 漏洞利用
    9.7. 持久化
    9.8. 防御
    9.9. 运维
    9.10. 其他
10. 手册速查
    10.1. 爆破工具
    10.2. 下载工具
    10.3. 流量相关
    10.4. 嗅探工具
    10.5. SQLMap使用
11. 其他
    11.1. 代码审计
    11.2. WAF
    11.3. Unicode
    11.4. 拒绝服务攻击
    11.5. Docker

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
