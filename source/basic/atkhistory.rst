网络攻防技术演化
========================================

历史发展
----------------------------------------
1939年，图灵破解了Enigma，使战争提前结束了两年，这是较早的一次计算机安全开始出现在人们的视野中，这个时候计算机的算力有限，人们使用的攻防方式也相对初级。

1949年，约翰·冯·诺依曼（John Von Neumann）提出了一种可自我复制的程序的设计，这被认为是世界上第一种计算机病毒。

1970年到2009年间，随着因特网不断发展，网络安全也开始进入人们的视野。在网络发展的初期，很多系统都是零防护的，安全意识也尚未普及开来。很多系统的设计也只考虑了可用性，对安全性的考虑不多，所以在当时结合搜索引擎与一些集成渗透测试工具，可以很容易的拿到数据或者权限。

1972年，缓冲区溢出攻击被 Computer Security Technology Planning Study 提出。

1984年，Ken Thompson 在 Reflections on Trusting Trust 一文中介绍了自己如何在编译器中增加后门来获取 Unix 权限的，这也是较早的供应链攻击。

1988年，卡耐基梅隆大学(Carnegie Mellon University, CMU)的一位学生以测试的目的编写了Morris Worm，对当时的互联网造成了极大的损害。

同年，CMU的CERT Coordination Center (CERT-CC)为了处理Morris Worm对互联网造成的破坏，组成了第一个计算机紧急响应小组(Computer Emergency Response Team)，而后全球多个国家、地区、团体都构建了CERT、SRC等组织。

同样是在1988年，Barton Miller教授在威斯康星大学的 `计算机实验课上 <http://pages.cs.wisc.edu/~bart/fuzz/CS736-Projects-f1988.pdf>`_ ，首次提出Fuzz生成器(Fuzz Generator)的概念，用于测试Unix程序的健壮性，即用随机数据来测试程序直至崩溃。因此，Barton Miller教授也被多数人尊称为"模糊测试之父"。

1989年，C.J.Cherryh 发表了小说 The Cuckoo's Egg: Tracking a Spy Through the Maze of Computer Espionage ，这本书是作者根据追溯黑客攻击的真实经历改编，在书中提出了蜜罐技术的雏形。

1990年，一些网络防火墙的产品开始出现，此时主要是基于网络的防火墙，可以处理FTP等应用程序。

1993年起，Jeff Moss开始每年在美国内华达州的拉斯维加斯举办 DEFCON (也写做 DEF CON, Defcon, or DC, 全球最大的计算机安全会议之一) 。CTF (Capture The Flag) 比赛的形式也是起源于1996年的 DEFCON 。

1993年7月，Windows NT 3.1发布，引入了身份认证、访问控制和安全审计等安全控制机制，在此之前的 Windows 9x 内核几乎没有任何安全性机制。

1996年，Smashing the Stack For Fun and Profit发表，在堆栈的缓冲区溢出的利用方式上做出了开创性的工作。

1997年起，Jeff Moss开始举办 Black Hat ，以中立的立场进行信息安全研究的交流和培训，到目前为止，Black Hat 也会在欧洲和亚洲举行。

1998年12月，Jeff Forristal在一篇 `文章 <http://www.phrack.com/issues.html?issue=54&id=8>`_ 中提到了使用SQL注入的技巧攻击一个网站的例子，从此SQL注入开始被广泛讨论。

1999年1月21日-22日的第二届 Research with Security Vulnerability Databases 的 WorkShop 上， MITRE 的创始人 David E. Mann 和 Steven M. Christey 发表了一篇名为《Towards a Common Enumeration of Vulnerabilities》的白皮书，提出了CVE (Common Vulnerabilities and Exposures, 通用漏洞披露) 的概念，在当年收录并公开了321个CVE漏洞。

1999年12月，MSRC的一些工程师发现了一些网站被注入代码的例子，他们在整理讨论后公开了这种攻击，并称为 Cross Site Scripting。

2002年1月，Microsoft发起了 “可信赖计算” (Trustworthy Computing) 计划，以帮助确保产品和服务在本质上具有高度安全性，可用性，可靠性以及业务完整性，SDL (Security Development Lifecycle) 也在此时被提出。

2001年9月9日，Mark Curphey启动了OWASP (Open Web Application Security Project) 项目，开始在社区中提供一些Web攻击技术的文章、方法和工具等。

在此之后，Responsible disclosure / Full disclosure 等概念也不断进入人们的视野之中。

2002年10月4日，Kevin Mitnick 编著的 The Art of Deception (欺骗的艺术) 出版，这本书详细的介绍了社会工程学在攻击中是如何应用的，Kevin Mitnick 也被认为是社会工程学的开山鼻祖。

2005年7月25日，Zero Day Initiative (ZDI) 创建，鼓励负责任的漏洞披露。

2005年11月，基于从1941年2月开始的情报收集积累和发展，Director of National Intelligence 宣布成立 Open Source Center (OSC) ，进行开源情报的收集，而后 Open-source intelligence (OSINT) 的概念也不断被人们认知。

2006年，APT(Advanced Persistent Threat, 高级持续威胁) 攻击的概念被正式提出，用来描述从20世纪90年代末到21世纪初在美国军事和政府网络中发现的隐蔽且持续的网络攻击。

2006年起，美国国土安全部（DHS）开始每两年举行一次 “网络风暴” (Cyber Storm) 系列国家级网络事件演习。

随着时代不断的发展，攻防技术有了很大的改变，防御手段、安全意识也随着演化。在攻击发生前有威胁情报、黑名单共享等机制，威胁及时能传播。在攻击发生时有基于各种机制的防火墙如关键字检测、语义分析、深度学习，有的防御机制甚至能一定程度上防御零日攻击。在攻击发生后，一些关键系统系统做了隔离，攻击成果难以扩大，就算拿到了目标也很难做进一步的攻击。也有的目标蜜罐仿真程度很高，有正常的服务和一些难以判断真假的业务数据。

2010年6月，震网 (Stuxnet) 被发现，在这之后供应链攻击事件开始成为网络空间安全的新兴威胁之一。随后的XcodeGhost、CCleaner等供应链攻击事件都造成了重大影响。

在2010年Forrester Research Inc.的分析师提出了“零信任”的概念模型时。

2012年1月，Gartner 公司提出了 IAST (Interactive Application Security Testing) 的概念，提供了结合 DAST 和 SAST 两种技术的解决方案。这种方式漏洞检出率高、误报率低，同时可以定位到API接口和代码片段。

2012年9月，Gartner 公司研究员 David Cearley 提出了 DevSecOps 的概念，表示 DevOps 的流程应该包含安全理念。

2013年，MITRE 提出了 ATT&CK™ (Adversarial Tactics, Techniques, and Common Knowledge, ATT&CK) ，这是一个站在攻击者的视角来描述攻击中各阶段用到的技术的模型。

2013年，Michigan 大学开始了 ZMap 项目，在2015年这个项目演化为 Censys ，从这之后网络空间测绘的项目逐渐出现。

2014年，在 Gartner Security and Risk Management Summit 上，Runtime Application Self-protection (RASP) 的概念被提出，在应用层进行安全保护。

2015年，Gartner 首次提出了 SOAR 的概念，最初的定义是 Security Operations, Analytics and Reporting，即安全运维分析与报告。

2017年，Gartner 对 SOAR 概念做了重新定义：Security Orchestration, Automation and Response, 即安全编排、自动化与响应。

参考链接
----------------------------------------
- `OWASP <https://en.wikipedia.org/wiki/OWASP>`_
- `NT Web Technology Vulnerabilities <http://www.phrack.com/issues.html?issue=54&id=8>`_
- `History of CVE <https://cve.mitre.org/about/history.html>`_
- `history of some vulnerabilities and exploit techniques <https://documents.pub/document/history-of-some-vulnerabilities-and-exploit-techniques.html>`_
- `securitydigest <http://securitydigest.org/>`_
- `Early Computer Security Papers: Ongoing Collection  <http://seclab.cs.ucdavis.edu/projects/history/CD/>`_
- `Security Mailing List Archive <https://seclists.org/>`_
- `Computer Security Technology Planning Study <https://csrc.nist.gov/csrc/media/publications/conference-paper/1998/10/08/proceedings-of-the-21st-nissc-1998/documents/early-cs-papers/ande72.pdf>`_
- `Smashing The Stack For Fun And Profit <https://inst.eecs.berkeley.edu/~cs161/fa08/papers/stack_smashing.pdf>`_
- `Happy 10th birthday Cross-Site Scripting! <https://docs.microsoft.com/en-us/archive/blogs/dross/happy-10th-birthday-cross-site-scripting>`_
- `About Microsoft SDL <https://www.microsoft.com/en-us/securityengineering/sdl/about>`_
- `ABOUT ZDI <https://www.zerodayinitiative.com/about/>`_
- `Open-source intelligence <https://en.wikipedia.org/wiki/Open-source_intelligence>`_
- `Runtime Application Self-protection (RASP) <https://www.gartner.com/en/information-technology/glossary/runtime-application-self-protection-rasp>`_
- `ZMap: Fast Internet-Wide Scanning and its Security Applications <https://zmap.io/paper.pdf>`_
- `A Search Engine Backed by Internet-Wide Scanning <https://censys.io/static/censys.pdf>`_
- `Black hat About <https://www.blackhat.com/about.html>`_
- `The DEF CON Story <https://www.defcon.org/html/links/dc-about.html>`_
- `Reflections on Trusting Trust <https://users.ece.cmu.edu/~ganger/712.fall02/papers/p761-thompson.pdf>`_
- `What is DevSecOps? <https://www.devsecops.org/blog/2015/2/15/what-is-devsecops>`_
