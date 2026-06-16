# Web Hacking Study Notes

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

[中文版 README](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/README.md) 

[Link to notes](https://websec.readthedocs.io)

# About
---
After diving into the vast ocean of cybersecurity knowledge, I realized that many topics and concepts are scattered and unorganized. Learning becomes unnecessarily difficult without a well-laid-out structure or guide. After grasping the basics, I attempted to gather and record these concepts, which eventually led to the creation of these notes. I hope they can help readers who are planning to learn web hacking.

Before starting, the question "what is web hacking?" needs to be answered. Web hacking covers a range of topics, including websites, web applications, web services, and more. In other words, web hacking focuses on application security and interactive systems. The necessary knowledge includes network protocols, the properties of network applications, their security risks, and the use of various applications. These categories can be complicated, so the following structure attempts to break down and reorganize the relevant content for easier understanding.

To better understand why the field of web security looks the way it does today, and where each area of study is headed, it is necessary to understand the history and evolution of web applications and network attack and defense technologies. This is the first part of the notes, focusing on the evolution of web technologies and the basics of the security field.

The second part introduces the basics of computer networks. Considering the many branches of databases, web servers, and the rapid evolution of the field, only network protocols are covered here. The skipped parts related to network applications should be understood together with programming languages, web application frameworks, network services, and operating system features.

With this foundation, the focus shifts to more detailed attack and defense topics, such as vulnerability types, programming languages, application characteristics, and their corresponding security issues. This is the third part of the notes. It briefly covers information gathering, common web vulnerabilities, languages and frameworks, and techniques for intranet penetration testing. Cloud technology is also important because it has become a key part of the web world. Whether using public cloud services, private clouds, or container technologies, cloud-related knowledge is becoming increasingly important.

The fourth part returns to the defensive perspective, describing security team building, threat intelligence, risk control, and more detailed technical topics such as honeypots and traceability.

The last part focuses on the introduction and use of applications. It includes recommended applications and resources, along with content that is currently unclassified.

The above is an overall summary of the content, but the reading order is not mandatory. Readers can start from any topic of interest. This compilation can be used both as a full set of notes and as a handbook.

Since the author is also still learning, mistakes or incomplete explanations are inevitable while organizing these notes. Errors will be fixed and information will be added in a timely manner. If you find any mistakes, you are welcome to report or correct them through an [Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new) or [PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls). Help is much appreciated.

Many sources were used as references when making these notes, and the corresponding links are listed at the end of each article. Many thanks to the authors for sharing these articles. The online version of these notes can be viewed [here](https://websec.readthedocs.io).

It is important to note that the English translation is still incomplete. Readers can use the translated [table of contents](#table-of-contents) as a reference for finding specific topics and read untranslated notes with the help of a translator.

# Table of Contents
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
3. Information collection (信息收集)
    1. Network architecture (网络整体架构)
    2. Domain (域名信息)
    3. Ports （端口信息）
    4. Website (站点信息)
    5. Search engine usage (搜索引擎利用)
    6. Social engineering (社会工程学)
    7. Reference Links (参考链接)
4. Common vulnerability offensive and defensive techniques (常见漏洞攻防）
    1. SQL injection (SQL注入)
    2. XSS
    3. CSRF
    4. SSRF
    5. Command injection (命令注入)
    6. directory traversal (目录穿越)
    7. File Reading (文件读取)
    8. File upload (文件上传)
    9. File contained (文件包含)
    10. XXE
    11. Template injection (模版注入)
    12. Xpath injection (Xpath注入)
    13. Logic/business vulnerability (逻辑漏洞 / 业务漏洞()
    14. Hardware safety (配置安全)
    15. Middleware (中间件)
    16. Web cache deception (Web Cache欺骗攻击)
    17. HTTP request smuggling (HTTP 请求走私)
5. Language and framework (语言与框架)
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
6. Intranet penetration (内网渗透)
    1. Windows intranet penetration (Windows内网渗透)
    2. Linux intranet penetration (Linux内网渗透)
    3. Backdoor technology 后门技术
    4. General techniques (综合技巧)
    5. Reference links (参考链接)
7. Cloud security (云安全)
    1. Container properties (容器标准)
    2. Docker
    3. Reference links (参考链接)
8. Defense techniques (防御技术)
    1. Team building (团队建设)
    2. Red/Blue teaming (红蓝对抗)
    3. Security development (安全开发)
    4. Security construction (安全建设)
    5. Threat intelligence (威胁情报)
    6. ATT&CK
    7. Risk control (风险控制)
    8. Defensive framework (防御框架)
    9. Reinforcement inspection (加固检查)
    10. Intrusion Detection (入侵检测)
    11. Zero-trust security (零信任安全)
    12. Honeypot technology (蜜罐技术)
    13. RASP
    14. Emergency Response (应急响应)
    15. Traceability Analysis (溯源分析_
9. Authentication mechanism (认证机制)
    1. Multi-factor authentication (多因子认证)
    2. SSO
    3. JWT
    4. OAuth
    5. SAML
    6. SCRAM
    7. Windows
    8. Kerberos
    9. NT LAN Manager (NTLM 身份验证)
10. Tools & Resources (工具与资源)
    1. Recommended resources (推荐资源)
    2. Relevant articles (相关论文)
    3. Information collection (信息收集)
    4. Social engineering (社会工程学)
    5. Fuzzing (模糊测试)
    6. Vulnerability exploitation/testing (漏洞利用/测试)
    7. Local infiltration (近源渗透)
    8. Web persistence (Web持久化)
    9. Lateral movement (横向移动)
    10. Cloud security (云安全)
    11. Operating system persistence (操作系统持久化)
    12. Audit tools (审计工具)
    13. Defense (防御)
    14. Security development (安全开发)
    15. Operation and maintenance (运维)
    16. Forensic (取证)
    17. Others (其他)
11. Handbook quicksearch (手册速查)
    1. Blasting tools (爆破工具)
    2. Download tools (下载工具)
    3. Flow related (流量相关)
    4. Sniffing tools (嗅探工具)
    5. SQLMap Usage (SQLMap使用)
12. Other (其他)
    1. Code audit (代码审计)
    2. WAF
    3. Common Networking Devices (常见网络设备)
    4. Fingerprints (指纹)
    5. Unicode
    6. JSON
    7. Denial of Service Attacks (拒绝服务攻击)
    8. Email Security (邮件安全)
    9. APT
    10. Supply Chain Security (供应链安全)
    11. Local infiltration (近源渗透)
    12. Commonly used Jargons (常见术语)

### Local Editing
---
```bash
git clone https://github.com/LyleMi/Learn-Web-Hacking.git
cd Learn-Web-Hacking
pip install sphinx sphinx-rtd-theme
make html
```
### Contributions
---

Questions and suggestions are welcome through issues or pull requests.

For English translation contributions, please treat the Chinese files under `source/` as the canonical source. English text should be maintained in `locale/en/LC_MESSAGES/*.po` rather than by copying or restructuring the source documents. After Chinese source content changes, regenerate gettext templates first, then update the English translation files with `sphinx-intl update`.

```bash
python -m sphinx -b gettext source build/gettext
sphinx-intl update -p build/gettext -l en
```

Thanks to all who [contributed](https://github.com/LyleMi/Learn-Web-Hacking/graphs/contributors).

### License
---

Published under the CC0 1.0 license. Click [here](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/LICENSE) to view it.

### Note
---

The content of these notes is collected and organized from open source information, and the technologies mentioned are for learning, authorized testing, and other legal scenarios only. For public safety reasons, some content is not included. Readers are requested to comply with the [Cybersecurity Law of the People's Republic of China](http://www.npc.gov.cn/npc/xinwen/2016-11/07/content_2001605.htm), the Regulations of the People's Republic of China on Computer Software Protection, and other applicable laws and regulations. Do not perform any kind of testing against unauthorized targets.
