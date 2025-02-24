Traceability analysis
========================================

Attack aircraft traceability technology
----------------------------------------

Log-based traceability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use routers, hosts and other devices to record key information (time, source address, destination address) in the data stream transmitted by the network, and reverse tracking is performed based on log queries when tracking.

The advantages of this method are strong compatibility, support for post-traceability, and have small network overhead. However, this method is also limited by performance, space and privacy protection. Taking into account the above factors, the recorded data characteristics and number of data can be limited. In addition, technologies such as traffic mirroring can be used to reduce the impact on network performance.

Routing input debugging technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In scenarios where the attack continues to send data and the characteristics are relatively stable, the router's input debugging technology can be used to dynamically track upwards when matching the attack traffic. This method is more effective in DDoS attack traceability and has a small network overhead.

Controllable flood technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When tracing, flood attacks are carried out to potential upstream routers. If the attack traffic is found to be reduced, the attack traffic will flow through the corresponding route. The advantage of this method is that it does not require pre-deployment and requires less coordination. But this method itself is an attack that will have some impact on the network.

Traceability technology based on package data modification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This traceability method directly modifies the data packet, adds encoding or tagging information, and reconstructs the transmission path at the receiving end. This method has less manpower investment and supports post-fact analysis, but it is not very supportive of some protocols.

Based on this method, random marking technology has been derived. Each route identifies data packets with a certain probability, and the receiver collects multiple packets and reconstructs them.

Based on honeypot traceability
----------------------------------------
- Social Network jsonp API
- Get the attacker's IP
- Get burp information

Analytical Model
----------------------------------------

Kill Kain model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The concept of kill chain originates from the military field and is a model that describes the attack link. Generally, kill chains include reconnaissance, weapon construction, payload delivery, exploitation, installation and implantation, communication control, and achievement of goals. Several stages.

The earlier the kill chain link prevents the attack, the better the protection effect, so the concept of the kill chain can also be used to counter attacks.

During the tracking phase, attackers usually use scanning and search methods to find possible target information and evaluate the cost of the attack. At this stage, you can discover it through log analysis, email analysis, etc., and at this stage, you can also use threat intelligence and other methods to obtain attack information.

During the weapon construction stage, the attacker usually has prepared the attack tools and conducts attempted attacks. At this stage, there may be attack records in IDS, and accounts such as external network applications and email addresses may have password explosion records. Some attackers will use public attack tools that will carry certain known characteristics.

During the payload delivery stage, attackers usually use network vulnerabilities, harpoons, puddles, network hijacking, USB flash drives and other methods to deliver malicious code. At this stage, some personnel have received attack payloads in the corresponding channels, and sufficient safety training for personnel can achieve a certain degree of defense.

During the breakthrough and utilization stage, the attacker will execute malicious code to obtain system control permissions. At this time, the Trojan program has been executed. At this stage, the corresponding attack can be found by relying on antivirus software, abnormal behavior alarms, etc.

During the installation and implantation phase, attackers usually install Webshell or implant backdoors, rootkits, etc. on the web server to achieve persistence control of the server. These implants can be found by reverse engineering the samples.

During the communication control phase, the attacker has implemented remote communication control, and the Trojan will communicate with the control server through three-party Web websites, DNS tunnels, mails, etc. At this time, you can find traces of the Trojan horse by analyzing the log.

When the target phase is achieved, the attacker begins to achieve his purpose, which may be to disrupt the normal operation of the system, steal target data, extort, lateral movement, etc. At this time, there may be an attack tool uploaded by an attacker in the controlled machine. At this stage, you can use honeypots and other methods to discover it.

Diamond model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The diamond model was proposed in 2013 by Sergio Catagirone and others from the Cyber Intelligence Analysis and Threat Research Institute (CCIATR).

The model divides all security events into four core elements, namely Adversary, Capability, Infrastructure and Victim, and uses diamond-shaped connections to represent their relationships , hence the name "Diamond Model".

The kill chain model is characterized by explaining the attack line and the process of the attack, while the diamond model is characterized by explaining the attacker's purpose and attack methods in a single event.

When using diamond model analysis, the fulcrum analysis method is usually used. Pivoting refers to the analysis technique that extracts an element and uses it to combine it with a data source to discover related elements. The fulcrum can be changed at any time in analysis, and the four core features and two extended features (social politics, technology) may all become the fulcrum of analysis at that time.

Correlation analysis method
----------------------------------------
Correlation analysis is used to combine multiple different attack samples.

Documentation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- hash
- ssdeep
- Version information (Company/Author/Last Modified Author/Creation Time/Last Modified Time)

Behavioral Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Based on network behavior
- Similar interaction methods

Executable file similarity analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Special port
- Special string/key
- PDB file path
- Similar folders
- Code reuse
- Similar code snippets

Clear logging method
----------------------------------------
-``kill <bash process ID>`` will not be stored
- ``set +o history`` does not write history
- ``unset HISTFILE`` Clears the history of environment variables

Reference link
----------------------------------------
- `Honey pot technology that uses social accounts to accurately trace the source <https://mp.weixin.qq.com/s/vlr2X68tMTgDhdDk4aow0g>`_
