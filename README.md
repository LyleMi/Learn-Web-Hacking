# Web安全学习笔记

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

### 序言
---

在学习Web安全的过程中，深切地感受到相关的知识浩如烟海，而且很大一部分知识点都相对零散，如果没有相对清晰的脉络作为参考，会给学习带来一些不必要的负担。于是在这之后尝试把一些知识、想法整理记录下来，最后形成了这份笔记。希望这份笔记能够为正在入门的网络安全爱好者提供一定的帮助。

笔记内容总体分为四个部分。第一部分围绕一些基础知识和技巧进行了一定的说明，主要包括Web技术的发展与演化、安全领域的基本常识、计算机网络的基础知识等，这些知识是进行Web安全学习的基础。第二部分按照常见的渗透测试的顺序，对信息收集、常见的Web漏洞、常见语言与框架、内网渗透的技巧等进行了简单的讲述，开始学习渗透测试之后通常会接触到这部分内容。第三部分回到防御的视角，从安全团队的建设、威胁情报与风控等视角进行了描述，也对蜜罐、溯源等较为细节的技术内容作了一定说明。最后一部分推荐了一些工具与资源列表，也归档了一部分暂时没有分类的内容。

笔者所学浅薄、精力有限，在整理笔记的过程中难免存在一些错误或是不完整的部分，正在逐步修正和补充。如果存在疏漏、错误，欢迎各位读者以[Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new)或者[PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls)的方式批评指正，感激不尽。

在编写笔记的过程中参考、摘抄了很多资料，都在文末留下了相应的链接，十分感谢文章作者的分享。其中笔记的在线版本可以点击[这里](https://websec.readthedocs.io)查看。

### 笔记大纲
---

1. 序章
    1. Web技术演化
    2. 网络攻防技术演化
    3. 安全观
2. 计算机网络与协议
    1. 网络基础
    2. UDP协议
    3. TCP协议
    4. 路由算法
    5. 域名系统
    6. HTTP标准
    7. HTTPS
    8. SSL/TLS
    9. IPsec
    10. Wi-Fi
3. 信息收集
    1. 网络整体架构
    2. 域名信息
    3. 端口信息
    4. 站点信息
    5. 搜索引擎利用
    6. 社会工程学
4. 常见漏洞攻防
    1. SQL注入
    2. XSS
    3. CSRF
    4. SSRF
    5. 命令注入
    6. 目录穿越
    7. 文件读取
    8. 文件上传
    9. 文件包含
    10. XXE
    11. 模版注入
    12. Xpath注入
    13. 逻辑漏洞 / 业务漏洞
    14. 配置安全
    15. 中间件
    16. Web Cache欺骗攻击
    17. HTTP 请求走私
5. 语言与框架
    1. PHP
    2. Python
    3. Java
    4. JavaScript
    5. Golang
    6. Ruby
    7. ASP
    8. PowerShell
    9. Shell
6. 内网渗透
    1. 信息收集 - Windows
    2. 持久化 - Windows
    3. 痕迹清理 - Windows
    4. 域渗透
    5. 信息收集 - Linux
    6. 持久化 - Linux
    7. 痕迹清理 - Linux
    8. 后门技术
    9. 综合技巧
    10. 参考链接
7. 防御技术
    1. 团队建设
    2. 安全开发
    3. 威胁情报
    4. ​​ATT&CK
    5. 风险控制
    6. 防御框架
    7. 加固检查
    8. 入侵检测
    9. 蜜罐技术
    10. RASP
    11. 应急响应
    12. 溯源分析
8. 认证机制
    1. SSO
    2. JWT
    3. OAuth
    4. SAML
    5. Windows
    6. Kerberos
    7. NTLM 身份验证
9. 工具与资源
    1. 推荐资源
    2. 相关论文
    3. 信息收集
    4. 社会工程学
    5. 模糊测试
    6. 漏洞利用
    7. 近源渗透
    8. Web持久化
    9. 横向移动
    10. 操作系统持久化
    11. 审计工具
    12. 防御
    13. 运维
    14. 其他
10. 手册速查
    1. 爆破工具
    2. 下载工具
    3. 流量相关
    4. 嗅探工具
    5. SQLMap使用
11. 其他
    1. 代码审计
    2. WAF
    3. Unicode
    4. 拒绝服务攻击
    5. Docker
    6. APT
    7. 近源渗透

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

笔记内容搜集整理自开源信息，仅供学习和交流参考。出于公共安全考虑，未收录部分内容，请读者遵守《[中华人民共和国网络安全法](http://www.npc.gov.cn/npc/xinwen/2016-11/07/content_2001605.htm)》，勿对非授权目标进行形式的测试。
