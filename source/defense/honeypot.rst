honeypot technology
========================================

Introduction
----------------------------------------
Honeypots are a deception technology for attackers, used to monitor, detect, analyze and trace attack behaviors. They have no business purpose. All traffic flowing into/out of honeypots indicates scanning or attack behaviors, so attack traffic can be better focused.

Honeypots can actively trap attackers, record many traces of the attacker's attack process in detail, and can collect a large amount of valuable data, such as the source code of viruses or worms, hacker operations, etc., thus facilitating the provision of rich traceability data. In addition, honeypots can also consume the attacker's time and obtain the attacker's portrait based on JSONP and other methods.

However, honeypots have security risks and may become a new source of attacks if they are not properly isolated.

Classification
----------------------------------------
According to the classification of uses, honeypots can be divided into research honeypots and product honeypots. Research honeypots are generally used to study various network threats and find ways to deal with them without increasing the security of a specific organization. Product honeypots are mainly commercial products used for protection.

According to the interaction method, honeypots can be divided into low-interaction honeypots and high-interaction honeypots. Low-interaction honeypots simulate network service responses and interact with attackers, making it easy to deploy and control attacks, but their simulation capabilities are relatively weak and their ability to capture attacks is not strong. High-interaction honeypots do not simply simulate protocols or services, but provide real systems, greatly reducing the probability of discovery. However, when high-interaction honeypots are not deployed properly, they may be exploited by attackers.

hidden technology
----------------------------------------
Honeypots mainly involve camouflage technology, which mainly involves process hiding, service camouflage and other technologies.

Hiding between honeypots requires honeypots to hide from each other. Process hiding, honeypot needs to hide monitoring, information collection and other processes. Pseudo service and command technology requires camouflaging some services to prevent attackers from obtaining sensitive information or intruding into the control core. Data file masquerading requires the generation of reasonably false data files.

Traction technology
----------------------------------------
Honeypot pulling technology is to draw the attacker to a specific honeypot address by changing the route in the formal environment and returning a specific response after identifying the attacker's traffic.
Common traction techniques include the following:

- Firewall pulling
- SDN traction
- ARP pulling
- WAF pulling

bait technology
----------------------------------------
Certain decoys can be deployed on the Internet to attract attackers into specific honeypots.
Common baits include domain name bait, Github bait, network disk bait, email bait, host bait, file bait, vulnerability bait, etc.

Domain name bait refers to using a specific main domain name that is meaningful in the dictionary as bait, such as ``vpn.example.com`` / ``oa.example.com``, etc.

Github bait refers to the way of placing code files and compromised credentials in Github.

File bait is a way of inducing attackers by placing false topology maps and files of key system IPs in easily compromised hosts.

Vulnerability bait attracts attackers to attack by deploying honeypot sites with specific vulnerability characteristics.

Countermeasures
----------------------------------------
Honeypots can use some methods to counterattack attackers. Common methods include Jsonp, security tool vulnerabilities, Client vulnerability countermeasures, file countermeasures, etc.

Jsonp mainly uses the Jsonp of major websites to obtain the social accounts that the attacker has logged in to trace the source.
In addition, if the attacker uses traffic to access the honeypot website, he can use the operator interface to obtain the attacker's mobile phone number.

Security tool vulnerabilities refer to the use of security tool vulnerabilities for countermeasures, such as file leak vulnerabilities in Git leak tools, XSS to RCE in Electron-based tools, etc.

Client countermeasures refer to using a fake server to counteract vulnerable clients, such as reading files through MySQL Client and performing RCE based on RDP/SMB vulnerabilities.

Countermeasure files refer to setting specific files in the honeypot environment, such as disguised VPN clients and specific plug-ins to induce attackers to click.

DoS countermeasures, after obtaining the attacker's C2 sample, can affect the C2 attacker's control server by going online in batches.

Identification technology
----------------------------------------
Attackers will also try to identify honeypots. It is easier to identify low-interaction honeypots. Trying some more complex and rare operations can make it easier to identify low-interaction honeypots. What is relatively difficult is the identification of high-interaction honeypots, because high-interaction honeypots are usually built based on real systems and are relatively close to real systems. This situation is usually identified based on virtual file system and registry information, memory allocation characteristics, hardware characteristics, special instructions, etc.

Protocol implementation identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During the implementation process of some honeypots, some parameters of the protocol have a limited fixed or random range, and honeypots can be identified by the range of specific parameters.

The version range supported by some honeypot protocols is a specific version range, and you can infer whether it is a honeypot based on the corresponding version range.

Some honeypots have interactions that detect client characteristics during the interaction process, and honeypots can be identified through these interaction processes.

Some honeypots also return normal responses to incorrect requests. This feature can be used to identify honeypots.

environmental characteristics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some honeypots have fixed usernames and passwords, or dynamic characteristics such as memory usage and process occupation change regularly. You can use this method to determine whether they are honeypots.

Reference link
----------------------------------------
- `honeypot wiki <https://en.wikipedia.org/wiki/Honeypot%5f%28computing%29>`_
- `Modern Honey Network <http://threatstream.github.io/mhn/>`_
- `Mo'an Technology: Magic Array <https://www.moresec.cn/magic-shield.html>`_
- `Honeypot and intranet security from 0 to 1 <https://xz.aliyun.com/t/998>`_
- `A brief analysis of open source honeypot identification and full network mapping <https://mp.weixin.qq.com/s?__biz=Mzk0NzE4MDE2NA==&mid=2247483908&idx=1&sn=e6a319e22c3cd54650bdbba511e58a43>`_
