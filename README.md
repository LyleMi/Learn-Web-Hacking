# Web Hacking Study Notes

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/license/lylemi/learn-web-hacking.svg)

[README](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/README.md) 

[Link to notes](https://websec.readthedocs.io)

# About
---
Upon diving into the vast ocean of knowledge about cybersecurity, I realized that many topics and concepts often are scattered and unorganized. Learning becomes unnecessarily difficult without a well-laid-out structure or guide. Thus after grasping the basics, attempted to gather concepts, record them and eventually lead to the creation of this note. The hope is that it can assist those who are planning to learn web hacking.

Before starting, the question of "what is web hacking?" needs to be answered. Frankly speaking, web hacking consists of a series of content, including topics such as websites, web applications, web services, and numerous more. In other words, web hacking focuses on the security of applications and the interactive level. The necessary knowledge of web hacking includes network protocols, properties of networking applications, their security risks, and the usage of various applications. These categories can be complicated, therefore try the following logic to disassemble and reorganize relevant contents for ease of understanding.

To better understand why the field of web security is the way it is now, and what direction each study is headed, it is necessary to understand the history of the development and evolution of web application and network attack and defense technologies. This is also the first part of the notes, focusing around the development and evolution of web technologies, and the basics of the security field.

The second part of this note introduces some of the basics of computer networks. Considering that there are many branches of databases, web servers, and the rapidly evolution of the field, only network protocols will be covered. The skipped part regarding network applications should be understood with the accompany of various programming languages, web application frameworks, network services and operating system features.

With some foundation, the focus shifts to some more detailed content on attack and defense, such as the study of vulnerability types, programming languages, characteristics of applications and their corresponding security issues. This is the third part of notes. A brief description is provided on information gathering, commonly seen web vulnerabitlites, languages and frameworks and techiniques on intranet penetration testing. Meanwhile there is also an importance in cloud technology as it becomes an important part of the web world. Whether it is using public cloud to build light services, private cloud. Technologies such as containers are becoming more and more important 

The fourth part returns to the defensive perspective, describing the construction of a security team, threat intelligence and risk control perspectives, as well as some description of more detailed technical content such as honeypots and traceability.

The last portion focuses on the introduction and usage of applications. Included is a list of recommendation for applications and resources, and some contents that are currently unclassified.

The above is the overall summerization of the content, but order is not mandatory. The topic can be from anywhere and start from anywhere of interest. This complilation can be used both as a whole and as a handbook.

Since the author is also studying, mistakes or incompleteness are inevitable in the process of organizing notes. Errors will fixed and information added in a timely fashion. If there exists any mistakes, readers are welcomed to criticize and correct them through [Issue](https://github.com/LyleMi/Learn-Web-Hacking/issues/new) or [PR](https://github.com/LyleMi/Learn-Web-Hacking/pulls). Help is much appreciated.

A lot of sources were used as reference in the making of these notes, all of which are left with the corresponding links at the end of the article. Many thanks to the authors for sharing these articles. Online versions of this notes can be viewed [here](https://websec.readthedocs.io)

It is important to note that only this Readme is translated at the moment. Readers can use the translated [table of contents](#table-of-contents) as reference in finding specific topics and read the notes with the help of an translator.

# table of contents
---
1. Prologue (序章)
    1. Evolution of networking technology
    2. Evolution of offensive and defensive networking technology
    3. Network Security perspective
    4. Laws and regulations
2. Computer networks and networking protocols
    1. networking fundamentals
    2. UDP protocol
    3. TCP protocol
    4. DHCP protocol
    5. Routing algorithms
    6. Domain name system
    7. HTTP protocol
    8. Simple Mail transfer protocol
    9. SSL/TLS
    10. IPsec
    11. Wi-Fi
3. information collection 
    1. Network architecture
    2. Domain
    3. Ports
    4. Website
    5. Search engine usage 
    6. Social engineering
    7. Reference Links
4. Common vulnerability offensive and defensive techiniques
    1. SQL injection
    2. XSS
    3. CSRF
    4. SSRF
    5. Command injection
    6. directory traversal
    7. File Reading
    8. File upload
    9. File contained
    10. XXE
    11. Template injection
    12. Xpath injection
    13. Logic/buiness vulnerability
    14. hardware safety
    15. middleware
    16. Web cache deception
    17. HTTP request smuggling
5. Language and framework
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
6. intranet penetration
    1. windows intranet penetration
    2. linus intranet penetration
    3. Backdoor technology
    4. General techiniques
    5. reference links
7. Cloud security
    1. Container properties
    2. Docker
    3. reference links
8. Defence techiniques
    1. Team building
    2. Red/Blue teaming
    3. Security development
    4. Security construction
    5. Threat intelligence
    6. ATT&CK
    7. Risk control
    8. Defensive framework
    9. Reinforcement inspection
    10. Intrusion Detection
    11. Zero-trust security
    12. Honeypot technology
    13. RASP
    14. Emergency Response
    15. Traceability Analysis
9. Authentication mechanism
    1. Multi-factor authentication
    2. SSO
    3. JWT
    4. OAuth
    5. SAML
    6. SCRAM
    7. Windows
    8. Kerberos
    9. NT LAN Manager
10. Tools & Resources 
    1. Recommanded Resources
    2. Relevant articles
    3. information collection
    4. Social engineering
    5. Fuzzing
    6. Vulnerability exploitation/testing
    7. local infiltration
    8. Web persistence
    9. Lateral movement
    10. Cloud security
    11. Operating system persistence
    12. audit tools
    13. defence
    14. Security development
    15. Operation and maintenance
    16. Forensic
    17. Others
11. Handbook quicksearch
    1. Blasting tools
    2. download tools
    3. Flow related
    4. sniffing tools
    5. SQLMap Usage
12. Other
    1. Code audit
    2. WAF
    3. Common Networking Devices
    4. Fingerprints
    5. Unicode
    6. JSON
    7. Denial of Service Attacks
    8. Email Security
    9. APT
    10. Supply Chain Security
    11. local infiltration
    12. Commonly used Jargons

### local editing 
---
```bash
git clone https://github.com/LyleMi/Learn-Web-Hacking.git
cd Learn-Web-Hacking
pip install sphinx sphinx-rtd-theme
make html
```
### Contributions
---

Questions and suggestions are welcomed through Issue or PR, much appreciated.

Thanks to all who [contributed](https://github.com/LyleMi/Learn-Web-Hacking/graphs/contributors).

### License
---

Published through license CC0 1.0, click [here](https://github.com/LyleMi/Learn-Web-Hacking/blob/master/LICENSE) to view

### note
---

The content of notes is collected and organized from open source information, and the technologies mentioned are for learning, authorized testing and other legal scenarios only. For public safety reasons, some of the content is not included. Readers are requested to comply with the legal provisions of the [Network Security Law of the People's Republic of China](http://www.npc.gov.cn/npc/xinwen/2016-11/07/content_2001605.htm), the Regulations of the People's Republic of China on Computer Software Protection, etc. and not to non-authorized targets for any kind of testing.
