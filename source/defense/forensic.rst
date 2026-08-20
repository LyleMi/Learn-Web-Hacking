Traceability analysis
========================================

Attack aircraft source tracing technology
----------------------------------------

Log-based traceability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use devices such as routers and hosts to record key information (time, source address, destination address) in the data flow transmitted over the network, and perform reverse tracing based on log queries during tracking.

The advantages of this method are strong compatibility, support for subsequent traceability, and low network overhead. However, this method is also limited by performance, space, and privacy protection. Considering the above factors, the recorded data characteristics and amount of data can be limited. In addition, technologies such as traffic mirroring can be used to reduce the impact on network performance.

Routing input debugging technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In a scenario where the attack continues to send data and the characteristics are relatively stable, the router's input debugging technology can be used to dynamically track upward when the attack traffic is matched. This method is more effective in DDoS attack tracing and has less network overhead.

controlled flooding technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During tracing, a flooding attack is performed on potential upstream routers. If it is found that the received attack traffic decreases, the attack traffic will flow through the corresponding route. The advantage of this approach is that it does not require pre-deployment and requires less collaboration. However, this method itself is an attack and will have an impact on the network.

Based on package data modification traceability technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This traceability method directly modifies the data packet, adds coding or marking information, and reconstructs the transmission path at the receiving end. This method requires less manpower and supports post-hoc analysis, but it does not support certain protocols very well.

Based on this method, random marking technology is derived. Each route identifies data packets with a certain probability, and the receiving end collects multiple packets and reconstructs them.

Traceability based on honeypot
----------------------------------------
- Social network jsonp API
- Get attacker IP
- Get burp information

Analytical model
----------------------------------------

Kill Kain model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The concept of kill chain originates from the military field. It is a model that describes the attack links. The general kill chain includes several stages including Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command & Control, and Actions on Objective.

The earlier the attack is stopped in the kill chain, the better the protection will be, so the concept of the kill chain can also be used to counter attacks.

During the tracking phase, attackers usually use methods such as scanning and searching to find possible target information and evaluate the cost of the attack. At this stage, it can be discovered through log analysis, email analysis, etc. At this stage, threat intelligence and other methods can also be used to obtain attack information.

During the weapon construction phase, attackers have usually prepared attack tools and conducted tentative attacks. At this stage, there may be attack records in the IDS, and there may be password blasting records for external network applications, mailboxes, and other accounts. Some attackers will use public attack tools with certain known characteristics.

In the payload delivery stage, attackers usually use network vulnerabilities, harpoons, puddles, network hijacking, USB flash drives, etc. to deliver malicious code. At this stage, personnel have already received the attack payload through the corresponding channels. Sufficient security training for personnel can achieve a certain degree of defense.

In the penetration and exploitation stage, the attacker will execute malicious code to obtain system control permissions. At this time, the Trojan program has been executed. At this stage, you can rely on anti-virus software, abnormal behavior alarms, etc. to find the corresponding attacks.

During the installation and implantation phase, attackers usually install Webshell or implant backdoors, rootkits, etc. on the web server to achieve persistent control over the server. These implants can be found by reverse engineering the sample.

In the communication control stage, the attacker has achieved remote communication control. The Trojan will communicate with the control server through third-party Web websites, DNS tunnels, emails, etc. At this point, traces of the Trojan can be found by analyzing the logs.

When the target stage is reached, the attacker begins to complete his or her own goals, which may include disrupting the normal operation of the system, stealing target data, extortion, lateral movement, etc. At this time, the controlled machine may already have the attack exploit tool uploaded by the attacker. Honeypots and other methods can be used to discover it at this stage.

Diamond model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The diamond model was proposed by Sergio Catagirone and others from the Center for Cyber ​​Intelligence Analysis and Threat Research (CCIATR) in 2013.

This model divides all security events into four core elements, namely Adversary, Capability, Infrastructure and Victim, with diamond-shaped connections representing the relationships between them, hence the name "Diamond Model".

The characteristic of the kill chain model is that it can explain the attack line and the process of the attack, while the characteristic of the diamond model is that it can explain the attack purpose and attack method used by the attacker in a single incident.

When using the diamond model for analysis, fulcrum analysis is usually used. Pivoting refers to the analysis technique of extracting an element and combining it with data sources to discover related elements. The fulcrum can be changed at any time during analysis, and the four core characteristics and two extended characteristics (social politics, technology) may become the fulcrum of analysis at that time.

correlation analysis method
----------------------------------------
Correlation analysis is used to combine multiple different attack samples.

Document class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- hash
- ssdeep
- Version information (company/author/last modified author/creation time/last modified time)

behavioral analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Based on network behavior
    - Similar interaction methods

Executable file similarity analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Special port
- Special string/key
- PDB file path
    - similar folders
- Code reuse
    - Similar code snippets

clear log method
----------------------------------------
- ``kill <bash process ID>`` will not store
- ``set +o history`` does not write history records
- ``unset HISTFILE`` clears the history environment variable

Reference link
----------------------------------------
- `Honeypot technology that uses social accounts to accurately trace their origins <https://mp.weixin.qq.com/s/vlr2X68tMTgDhdDk4aow0g>`_
