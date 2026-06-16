# Web Hacking Study Notes

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

[中文版 README](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/README.md) 

[Link to notes](https://websec.readthedocs.io)

# English Translation Status
---
This English version is a work in progress. The translated table of contents is intended to help readers find topics, but many pages in the English site may still show the original Chinese text.

The Chinese files under `source/` remain the canonical source. English translation work should be maintained in `locale/en/LC_MESSAGES/*.po`, with terminology kept consistent with `locale/en/glossary.md`.

# About
---
After diving into the vast ocean of cybersecurity knowledge, I realized that many topics and concepts are scattered and unorganized. Learning becomes unnecessarily difficult without a well-laid-out structure or guide. After grasping the basics, I attempted to gather and record these concepts, which eventually led to the creation of these notes. I hope they can help readers who are planning to learn web hacking.

Before starting, the question "what is web hacking?" needs to be answered. Web hacking covers a range of topics, including websites, web applications, web services, and more. In other words, web hacking focuses on application security and interactive systems. The necessary knowledge includes network protocols, the properties of network applications, their security risks, and the use of various applications. These categories can be complicated, so the following structure attempts to break down and reorganize the relevant content for easier understanding.

To better understand why the field of web security looks the way it does today, and where each area of study is headed, it is necessary to understand the history and evolution of web applications and network attack and defense technologies. This is the first part of the notes, focusing on the evolution of web technologies and the basics of the security field.

The second part introduces the basics of computer networks. Considering the many branches of databases, web servers, and the rapid evolution of the field, only network protocols are covered here. The skipped parts related to network applications should be understood together with programming languages, web application frameworks, network services, and operating system features.

With this foundation, the focus shifts to more detailed attack and defense topics, such as vulnerability types, programming languages, application characteristics, and their corresponding security issues. This is the third part of the notes. It briefly covers information gathering, common web vulnerabilities, languages and frameworks, and internal network penetration techniques. Cloud technology is also important because it has become a key part of the web world. Whether using public cloud services, private clouds, or container technologies, cloud-related knowledge is becoming increasingly important.

The fourth part returns to the defensive perspective, describing security team building, threat intelligence, risk control, and more detailed technical topics such as honeypots and attribution analysis.

The last part focuses on the introduction and use of applications. It includes recommended applications and resources, along with content that is currently unclassified.

The above is an overall summary of the content, but the reading order is not mandatory. Readers can start from any topic of interest. This compilation can be used both as a full set of notes and as a handbook.

Since the author is also still learning, mistakes or incomplete explanations are inevitable while organizing these notes. Errors will be fixed and information will be added in a timely manner. If you find any mistakes, you are welcome to report or correct them through an [Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new) or [PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls). Help is much appreciated.

Many sources were used as references when making these notes, and the corresponding links are listed at the end of each article. Many thanks to the authors for sharing these articles. The online version of these notes can be viewed [here](https://websec.readthedocs.io).

# Table of Contents
---
1. Prologue (序章)
    1. Evolution of Web Technology (Web技术演化)
    2. Evolution of Network Attack and Defense Technology (网络攻防技术演化)
    3. Network Security Perspective (网络安全观)
    4. Laws and Regulations (法律与法规)
2. Computer Networks and Protocols (计算机网络与协议)
    1. Network Fundamentals (网络基础)
    2. UDP Protocol (UDP协议)
    3. TCP Protocol (TCP协议)
    4. DHCP Protocol (DHCP协议)
    5. Routing Algorithms (路由算法)
    6. Domain Name System (域名系统)
    7. HTTP Protocol Suite (HTTP协议簇)
    8. SSH
    9. Mail Protocol Suite (邮件协议族)
    10. SSL/TLS
    11. IPsec
    12. Wi-Fi
3. Information Gathering (信息收集)
    1. Network Architecture (网络整体架构)
    2. Domain Information (域名信息)
    3. Port Information (端口信息)
    4. Website Information (站点信息)
    5. Search Engine Usage (搜索引擎利用)
    6. Social Engineering (社会工程学)
    7. Reference Links (参考链接)
4. Common Vulnerability Attack and Defense (常见漏洞攻防)
    1. SQL Injection (SQL注入)
    2. XSS
    3. CSRF
    4. SSRF
    5. Command Injection (命令注入)
    6. Path Traversal (目录穿越)
    7. File Read (文件读取)
    8. File Upload (文件上传)
    9. File Inclusion (文件包含)
    10. XXE
    11. Template Injection (模版注入)
    12. XPath Injection (Xpath注入)
    13. Logic and Business Vulnerabilities (逻辑漏洞 / 业务漏洞)
    14. Configuration Security (配置安全)
    15. Middleware (中间件)
    16. Web Cache Deception (Web Cache欺骗攻击)
    17. HTTP Request Smuggling (HTTP 请求走私)
5. Languages and Frameworks (语言与框架)
    1. PHP
    2. Python
    3. Java
    4. JavaScript
    5. Golang
    6. Ruby
    7. ASP
    8. PowerShell
    9. Shell
    10. C#
6. Internal Network Penetration (内网渗透)
    1. Windows Internal Network Penetration (Windows内网渗透)
    2. Linux Internal Network Penetration (Linux内网渗透)
    3. Backdoor Techniques (后门技术)
    4. General Techniques (综合技巧)
    5. Reference Links (参考链接)
7. Cloud Security (云安全)
    1. Cloud History (云发展史)
    2. Container Standards (容器标准)
    3. Docker
    4. Kubernetes
    5. Reference Links (参考链接)
8. LLM Security (大模型安全)
    1. Basic Concepts (基本概念)
    2. Common Risks (常见风险)
    3. Common Attack Methods (常见攻击方式)
    4. Security Defense (安全防御)
    5. Testing Methods (检测方法)
    6. Reference Links (参考链接)
9. Defense Techniques (防御技术)
    1. Team Building (团队建设)
    2. Red/Blue Teaming (红蓝对抗)
    3. Security Development (安全开发)
    4. Security Construction (安全建设)
    5. Threat Intelligence (威胁情报)
    6. ATT&CK
    7. Risk Control (风险控制)
    8. Defensive Framework (防御框架)
    9. Hardening Assessment (加固检查)
    10. Intrusion Detection (入侵检测)
    11. Zero Trust Security (零信任安全)
    12. Honeypot Technology (蜜罐技术)
    13. RASP
    14. Incident Response (应急响应)
    15. Attribution Analysis (溯源分析)
10. Authentication Mechanisms (认证机制)
    1. Multi-factor Authentication (多因子认证)
    2. SSO
    3. JWT
    4. OAuth
    5. SAML
    6. SCRAM
    7. Windows
    8. Kerberos
    9. NT LAN Manager (NTLM 身份验证)
    10. Access Control System Design Model (权限系统设计模型)
11. Tools and Resources (工具与资源)
    1. Recommended Resources (推荐资源)
    2. Relevant Articles (相关论文)
    3. Information Gathering (信息收集)
    4. Social Engineering (社会工程学)
    5. Fuzzing (模糊测试)
    6. Vulnerability Exploitation and Testing (漏洞利用/测试)
    7. Proximity-based Penetration Testing (近源渗透)
    8. Web Persistence (Web持久化)
    9. Lateral Movement (横向移动)
    10. Cloud Security (云安全)
    11. Operating System Persistence (操作系统持久化)
    12. Audit Tools (审计工具)
    13. Defense (防御)
    14. Security Development (安全开发)
    15. Operations and Maintenance (运维)
    16. Forensics (取证)
    17. Others (其他)
12. Quick Reference (手册速查)
    1. Brute-force Tools (爆破工具)
    2. Download Tools (下载工具)
    3. Traffic-related Tools (流量相关)
    4. Sniffing Tools (嗅探工具)
    5. SQLMap Usage (SQLMap使用)
13. Other (其他)
    1. Code Audit (代码审计)
    2. WAF
    3. Common Network Devices (常见网络设备)
    4. Fingerprints (指纹)
    5. Unicode
    6. JSON
    7. Hashing (哈希)
    8. Denial of Service Attacks (拒绝服务攻击)
    9. Email Security (邮件安全)
    10. APT
    11. Supply Chain Security (供应链安全)
    12. Proximity-based Penetration Testing (近源渗透)
    13. Web Crawling (爬虫)
    14. Common Terminology (常见术语)
    15. ICS Security (工控安全)

### Local Editing
---
```bash
git clone https://github.com/LyleMi/Learn-Web-Hacking.git
cd Learn-Web-Hacking
pip install -r requirements.txt
make html-zh
make html-en
```
### Contributions
---

Questions and suggestions are welcome through issues or pull requests.

For English translation contributions, please treat the Chinese files under `source/` as the canonical source. English text should be maintained in `locale/en/LC_MESSAGES/*.po` rather than by copying or restructuring the source documents. After Chinese source content changes, regenerate gettext templates first, then update the English translation files with `sphinx-intl update`.

Use `locale/en/glossary.md` for preferred English terms and consistency rules before translating new sections.

```bash
make gettext
make i18n-en
make html-en
```

Thanks to all who [contributed](https://github.com/LyleMi/Learn-Web-Hacking/graphs/contributors).

### License
---

Published under the CC0 1.0 license. Click [here](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/LICENSE) to view it.

### Note
---

The content of these notes is collected and organized from open source information, and the technologies mentioned are for learning, authorized testing, and other legal scenarios only. For public safety reasons, some content is not included. Readers are requested to comply with the [Cybersecurity Law of the People's Republic of China](http://www.npc.gov.cn/npc/xinwen/2016-11/07/content_2001605.htm), the Regulations of the People's Republic of China on Computer Software Protection, and other applicable laws and regulations. Do not perform any kind of testing against unauthorized targets.
