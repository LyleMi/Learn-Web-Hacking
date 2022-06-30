# Network Security notes

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

[中文版 README（Chinese version ReadME）](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/README.md) 

[Link to notes](https://websec.readthedocs.io)

# About
---
Upon diving into the vast ocean of knowledge that is Network security, the author realized that many topics and concepts often are scattered and unorganized. Learning becomes unnecessarily difficult without a well layed out structure or guide. Thus after grasping the basics, attempted to gather concepts, record them and eventually lead to the creation of this note compilation. The hope is that it can assist those who are planning to learn network security.

Before starting, the question of "what is network security?" needs to be answered. Frankly speaking, network security consists of a series of content, including topics such as websites, web applications, web services and numerous more. In other words, network security focuses on the security of applications and the interactive level. The necessary knowledges of network security includes network protocols, properties of networking applications, their security risks and the usage of various applications. These catagories can be complicated, therefore try the following logic to disassemble and reorganize relevant contents for ease of understanding.

#

To better understand why the field of Web security is the way it is now, and what direction each study is headed, it is necessary to understand the history of the development and evolution of Web application and network attack and defense technologies. This is also the first part of the notes, focusing around the development and evolution of Web technologies, and the basics of the security field.

The second part of this compliation introduces some of the basics of computer networks. Considering that there are many branches of network databases, web servers, and the rapidly evolution of the field, only network protocols will be covered. The skipped part regarding network applications should be understood with the accompany of various programming languages, web application frameworks, network services and operating system features.

With some foundation, the focus shifts to some more detailed content on attack and defense, such as the study of vulnerability types, programming languages, characteristics of applications and their corresponding security issues. This is the third part of notes. A brief description is provided on information gathering, commonly seen Web vulnerabitlites, languages and frameworks and techiniques on penetration testing. Meanwhile there is also an importance in cloud technology as it becomes an important part of the web world. Whether it is using public cloud to build light services, private cloud. Technologies such as containers are becoming more and more important 

The fourth part returns to the defensive perspective, describing the construction of a security team, threat intelligence and risk control perspectives, as well as some description of more detailed technical content such as honeypots and traceability.

The last portion focuses on the introduction and usage of applications. Included is a list of recommendation for applications and resources, and some contents that are currently unclassified.

#
The above is the overall summerization of the content, but order is not mandatory. The topic can be from anywhere and start from anywhere of interest. This complilation can be used both as a whole and as a handbook.

As the author is also learning and is human, it is inevitable for errors or incompletes in the process of organizing notes. Errors will fixed and information added in a timely fashion. If there exists any mistakes, readers are welcomed to criticize and correct them through [Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new) or [PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls). Help is much appreciated.

A lot of sources were used as reference in the making of these notes, all of which are left with the corresponding links at the end of the article. Many thanks to the authors for sharing these articles. Online versions of the Network Security notes can be viewed [here](https://websec.readthedocs.io)

It is important to note that only this Readme is translated at the moment. Readers can use the translated [table of contents](#table-of-contents) as reference in finding specific topics and read the notes with the help of an translator.

# table of contents
---
1. Prologue (序章)
    1. Evolution of networking technology (Web技术演化)
    2. Evolution of offensive and defensive networking technology (网络攻防技术演化)
    3. Network Security perspective (安全观) 
    4. Laws and regulations (法律与法观）
2. Computer networks and networking protocols (计算机网络与协议)
    1. networking fundamentals (网络基础)
    2. UDP protocol (UDP协议)
    3. TCP protocol (TCP协议)
    4. DHCP protocol (DHCP协义）
    5. Routing algorithms (路由算法)
    6. Domain name system (域名系统)
    7. HTTP protocol (HTTP协议簇)
    8. Simple Mail transfer protocol (邮件协议族)
    9. SSL/TLS
    10. IPsec
    11. Wi-Fi
3. 信息收集
    1. 网络整体架构
    2. 域名信息
    3. 端口信息
    4. 站点信息
    5. 搜索引擎利用
    6. 社会工程学
    7. 参考链接
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
    10. Csharp
6. 内网渗透
    1. Windows内网渗透
    2. Linux内网渗透
    3. 后门技术
    4. 综合技巧
    5. 参考链接
7. 云安全
    1. 容器标准
    2. Docker
    3. 参考链接
8. 防御技术
    1. 团队建设
    2. 红蓝对抗
    3. 安全开发
    4. 安全建设
    5. 威胁情报
    6. ATT&CK
    7. 风险控制
    8. 防御框架
    9. 加固检查
    10. 入侵检测
    11. 零信任安全
    12. 蜜罐技术
    13. RASP
    14. 应急响应
    15. 溯源分析
9. 认证机制
    1. 多因子认证
    2. SSO
    3. JWT
    4. OAuth
    5. SAML
    6. SCRAM
    7. Windows
    8. Kerberos
    9. NTLM 身份验证
10. 工具与资源
    1. 推荐资源
    2. 相关论文
    3. 信息收集
    4. 社会工程学
    5. 模糊测试
    6. 漏洞利用/测试
    7. 近源渗透
    8. Web持久化
    9. 横向移动
    10. 云安全
    11. 操作系统持久化
    12. 审计工具
    13. 防御
    14. 安全开发
    15. 运维
    16. 取证
    17. 其他
11. 手册速查
    1. 爆破工具
    2. 下载工具
    3. 流量相关
    4. 嗅探工具
    5. SQLMap使用
12. 其他
    1. 代码审计
    2. WAF
    3. 常见网络设备
    4. 指纹
    5. Unicode
    6. JSON
    7. 拒绝服务攻击
    8. 邮件安全
    9. APT
    10. 供应链安全
    11. 近源渗透
    12. 常见术语
