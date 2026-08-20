Evolution of network attack and defense technologies
========================================

Historical development
----------------------------------------
In 1939, Turing cracked Enigma, ending the war two years early. This was the first time computer security began to appear in people's vision. At this time, the computing power of computers was limited, and the attack and defense methods used by people were relatively rudimentary.

In 1949, John Von Neumann proposed the design of a self-replicating program, which is considered the world's first computer virus.

From 1970 to 2009, with the continuous development of the Internet, network security also began to enter people's field of vision. In the early days of network development, many systems had zero protection, and security awareness had not yet become widespread. Many systems were designed with only usability in mind and not much consideration for security. Therefore, at that time, combining search engines with some integrated penetration testing tools made it easy to obtain data or permissions.

In 1972, the buffer overflow attack was proposed by the Computer Security Technology Planning Study.

In 1984, Ken Thompson introduced in Reflections on Trusting Trust how he added a backdoor to the compiler to obtain Unix permissions. This was also an early supply chain attack.

In 1988, a student at Carnegie Mellon University (CMU) wrote Morris Worm for testing purposes, which caused great damage to the Internet at that time.

In the same year, CMU's CERT Coordination Center (CERT-CC) formed the first Computer Emergency Response Team (Computer Emergency Response Team) in order to deal with the damage caused by Morris Worm to the Internet. Since then, many countries, regions, and groups around the world have established organizations such as CERT and SRC.

Also in 1988, Professor Barton Miller first proposed the concept of Fuzz Generator in his computer experiment class at the University of Wisconsin <http://pages.cs.wisc.edu/~bart/fuzz/CS736-Projects-f1988.pdf>`_, which was used to test the robustness of Unix programs, that is, to use random data to test the program until it crashes. Therefore, Professor Barton Miller is also revered as the "Father of Fuzz Testing" by most people.

In 1989, C.J. Cherryh published the novel The Cuckoo's Egg: Tracking a Spy Through the Maze of Computer Espionage. This book was adapted from the author's real experience of tracing hacker attacks. In the book, he proposed the prototype of honeypot technology.

In 1990, some network firewall products began to appear. At this time, they were mainly network-based firewalls that could handle applications such as FTP.

Since 1993, Jeff Moss has held DEFCON (also written as DEF CON, Defcon, or DC, one of the world's largest computer security conferences) every year in Las Vegas, Nevada, USA. The format of the CTF (Capture The Flag) competition also originated from DEFCON in 1996.

In July 1993, Windows NT 3.1 was released, which introduced security control mechanisms such as identity authentication, access control, and security auditing. Prior to this, the Windows 9x kernel had almost no security mechanisms.

In 1996, Smashing the Stack For Fun and Profit was published, and he did pioneering work on how to exploit stack buffer overflows.

Since 1997, Jeff Moss has started organizing Black Hat to conduct information security research exchanges and training from a neutral standpoint. So far, Black Hat will also be held in Europe and Asia.

In December 1998, Jeff Forristal mentioned an example of using SQL injection techniques to attack a website in an article <http://www.phrack.com/issues.html?issue=54&id=8>`_. Since then, SQL injection has been widely discussed.

At the second Research with Security Vulnerability Databases WorkShop from January 21 to 22, 1999, MITER founders David E. Mann and Steven M. Christey published a white paper titled "Towards a Common Enumeration of Vulnerabilities", proposing the concept of CVE (Common Vulnerabilities and Exposures, Common Vulnerability Disclosure). In that year, 321 CVE vulnerabilities were included and disclosed.

In December 1999, some MSRC engineers discovered some examples of websites being injected with code. After collating discussions, they disclosed this attack and called it Cross Site Scripting.

In January 2002, Microsoft launched the "Trustworthy Computing" program to help ensure that products and services are inherently highly secure, available, reliable, and business complete. SDL (Security Development Lifecycle) was also proposed at this time.

On September 9, 2001, Mark Curphey launched the OWASP (Open Web Application Security Project) project and began to provide some articles, methods, and tools on Web attack technologies in the community.

After that, concepts such as Responsible disclosure/Full disclosure have continued to come into people's vision.

On October 4, 2002, The Art of Deception edited by Kevin Mitnick was published. This book introduces in detail how social engineering is used in attacks. Kevin Mitnick is also considered the originator of social engineering.

On July 25, 2005, the Zero Day Initiative (ZDI) was created to encourage responsible vulnerability disclosure.

In November 2005, based on the accumulation and development of intelligence collection starting in February 1941, the Director of National Intelligence announced the establishment of the Open Source Center (OSC) to collect open source intelligence. Later, the concept of Open-source intelligence (OSINT) has been increasingly recognized.

In 2006, the concept of APT (Advanced Persistent Threat, Advanced Persistent Threat) attacks was formally proposed to describe the covert and persistent cyber attacks discovered in US military and government networks from the late 1990s to the early 21st century.

Since 2006, the U.S. Department of Homeland Security (DHS) has begun holding the “Cyber ​​Storm” series of national-level cyber incident exercises every two years.

With the continuous development of the times, offensive and defensive technologies have changed greatly, and defense methods and security awareness have also evolved. There are mechanisms such as threat intelligence and blacklist sharing before an attack occurs, so threats can spread in a timely manner. When an attack occurs, there are firewalls based on various mechanisms such as keyword detection, semantic analysis, and deep learning. Some defense mechanisms can even defend against zero-day attacks to a certain extent. After the attack occurred, some key systems were isolated, making it difficult to expand the results of the attack. Even if the target was obtained, it would be difficult to carry out further attacks. There are also target honeypots with a high degree of simulation, including normal services and some business data that is difficult to determine whether it is true or false.

In June 2010, Stuxnet was discovered. After that, supply chain attacks began to become one of the emerging threats to cyberspace security. Subsequent supply chain attacks such as XcodeGhost and CCleaner have had a major impact.

In 2010, analysts at Forrester Research Inc. proposed the conceptual model of “zero trust.”

In January 2012, Gartner proposed the concept of IAST (Interactive Application Security Testing), providing a solution that combines DAST and SAST technologies. This method has a high vulnerability detection rate and low false positive rate, and can locate API interfaces and code fragments at the same time.

In September 2012, Gartner researcher David Cearley proposed the concept of DevSecOps, saying that the DevOps process should include security concepts.

In 2013, MITER proposed ATT&CK™ (Adversarial Tactics, Techniques, and Common Knowledge, ATT&CK), which is a model that describes the techniques used in each stage of the attack from the attacker's perspective.

In 2013, the University of Michigan started the ZMap project, which evolved into Censys in 2015. Since then, cyberspace mapping projects have gradually emerged.

In 2014, at the Gartner Security and Risk Management Summit, the concept of Runtime Application Self-protection (RASP) was proposed to provide security protection at the application layer.

In 2015, Gartner first proposed the concept of SOAR. The initial definition was Security Operations, Analytics and Reporting, which means security operation and maintenance analysis and reporting.

In 2017, Gartner redefined the concept of SOAR: Security Orchestration, Automation and Response, that is, security orchestration, automation and response.

Reference link
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
