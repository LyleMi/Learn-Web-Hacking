Honeypot technology
========================================

Introduction
----------------------------------------
Honeypot is a deceptive technology for attackers, used to monitor, detect, analyze and trace attack behavior. It has no business purpose. All traffic flowing into/out of honeypot indicates scanning or attack behavior, so it can be better. Focus on attack traffic.

Honeypot can realize the active trapping of attackers, can record many traces of attackers in detail, and can collect a large amount of valuable data, such as viruses or worms source code, hackers' operations, etc., so as to provide rich Traceable data. In addition, honeypots can also consume the attacker's time and obtain the attacker's portrait based on JSONP and other methods.

However, honeypots have safety risks. If they are not isolated properly, they may become a new source of attack.

Classification
----------------------------------------
According to the purpose, honeypots can be divided into research-type honeypots and product-type honeypots. Research-type honeypots are generally used to study various cyber threats and find ways to deal with them without increasing the security of specific organizations. Product-type honeypots are mainly commercial products used for protection.

Classified by interaction, honeypots can be divided into low-interaction honeypots and high-interaction honeypots. Low-interaction honeypot simulates network service response and attacker interaction, making it easy to deploy and control attacks, but its simulation capabilities will be relatively weak and its ability to capture attacks is not strong. High interactive honeypots are not simply simulated protocols or services, but provide real systems, which greatly reduces the probability of being discovered. However, the deployment of high-interaction honeypots is incorrectly deployed at that time, and there is a possibility that they will be exploited by the attacker.

Hidden technology
----------------------------------------
Honeypot mainly involves camouflage technology, mainly involving process hiding and service camouflage technologies.

The hiding between honeypots requires that honeypots be hidden from each other. The process is hidden, and the honeypot needs to hide monitoring, information collection and other processes. Pseudo-service and command technology require some services to be disguised to prevent attackers from obtaining sensitive information or intruding into the control kernel. Data files are disguised and files that require reasonable false data are generated.

Traction technology
----------------------------------------
Honeypot traction technology is to pull the attacker to a specific honeypot address by changing the route in the formal environment and returning a specific response after identifying the attacker traffic.
There are several common traction techniques:

- Firewall traction
- SDN traction
- ARP traction
- WAF traction

Bait technology
----------------------------------------
A certain amount of bait can be deployed in the Internet to attract attackers into specific honeypots.
Common baits include domain name bait, Github bait, net disk bait, email bait, host bait, file bait, vulnerability bait, etc.

Domain name bait refers to the use of a specific main domain name that is meaningful in the dictionary as bait, such as ``vpn.example.com`` / ``oa.example.com``, etc.

Github Bait refers to the way to place code files and lost credentials in Github.

File bait is the way to induce attackers by placing fake topology maps, key system IP files in a host that is prone to lose.

Vulnerability Bait attracts attackers to attack by deploying honeypot stations with specific vulnerability characteristics.

Counter-response technology
----------------------------------------
Honeypot can use some methods to counter attackers. Common methods include Jsonp, security tool vulnerabilities, Client vulnerabilities counter, file counters, etc.

Jsonp mainly uses Jsonp from major websites to obtain the social account that the attacker has logged in to for traceability.
In addition, if an attacker uses traffic to access the honeypot website, he or she can use the operator interface to obtain the attacker's mobile number.

Security tool vulnerabilities refer to countering vulnerabilities using security tools, such as file leak vulnerabilities in Git leak tools, XSS to RCE in Electron-based tools, etc.

Client countermeasures refer to using fake Server to counter vulnerable clients, such as reading files through MySQL Client, and RCE based on RDP/SMB vulnerabilities.

Counter file refers to setting specific files in a honeypot environment, such as disguised VPN clients and specific plug-ins to induce attackers to click.

DoS countermeasures that after obtaining the attacker's C2 samples, it can affect the C2 attacker's control server through batch launch.

Identification technology
----------------------------------------
The attacker will also try to identify the honeypot. The one that is easier to identify is the honeypot with low interaction. Try some more complex and rare operations to easily identify the honeypot with low interaction. What is relatively difficult is the recognition of high-interactive honeypots, because high-interactive honeypots are usually built on a real system and are relatively similar to real systems. In this case, it is usually identified based on information of the virtual file system and registry, memory allocation features, hardware features, special instructions, etc.

Protocol implementation identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During the implementation of some honeypots, the protocol has a fixed or random range of partial parameters, and the honeypot can be identified by the range of specific parameters.

Some honeypot protocols support version ranges for a specific version range, and you can guess whether it is a honeypot based on the corresponding version range.

Some honeypots have interactions that detect client characteristics during the interaction process, and honeypots can be identified through these interaction processes.

Some honeypots also return normal responses for incorrect requests. This feature can be used to determine the honeypot.

Environmental characteristics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some honeypots have relatively regular changes in dynamic characteristics such as username and password, or memory usage and process occupation. This method can be used to determine whether they are honeypots.

Reference link
----------------------------------------
- `honeypot wiki <https://en.wikipedia.org/wiki/Honeypot%5f%28computing%29>`_
- `Modern Honey Network <http://threatstream.github.io/mhn/>`_
- `Moan Technology: Magic Array <https://www.moresec.cn/magic-shield.html>`_
- `Honeypot and intranet security from 0 to 1 <https://xz.aliyun.com/t/998>`_
- `Simple analysis of open source honeypot identification and network mapping <https://mp.weixin.qq.com/s?__biz=Mzk0NzE4MDE2NA==&mid=2247483908&idx=1&sn=e6a319e22c3cd54650bdbba511e58a43>`_
