Denial of Service Attack
========================================

Introduction
----------------------------------------
DoS (Denial of Service) refers to denial of service, which is a cyber attack method commonly used to paralyze servers or networks.

In normal times, more is the distributed denial of service (DDoS) attack. This attack refers to using a sufficient number of puppet computers to generate a large number of attack data packets to target one or more targets on the network. Implementing DDoS attacks increases the power exponentially, thereby exhausting the resources of the victim target and forcing the target to lose its ability to provide normal services.

UDP reflection
----------------------------------------
Reflective DDoS attack based on UDP articles is a form of denial of service attack. The attacker does not directly attack the target, but uses some open servers on the Internet to forge the address of the attacked person and send special request messages based on UDP service to the server, so that data that is several times more than the request messages are sent to The IP is attacked, thereby indirectly forming a DDoS attack on the latter.

Services commonly used for DoS attacks include:

- NTP
- DNS
- SSDP
- Memcached

Among them, DNS attacks mainly refer to DNS Request Flood, DNS Response Flood, false source + real source DNS Query Flood, authoritative server attacks and Local server attacks.

TCP Flood
----------------------------------------
TCP Flood is an attack that takes advantage of the defects of TCP protocol. This method sends a large number of forged TCP SYN requests to the attacking server through forged IP. After the attacked server responds to the handshake packet (SYN+ACK), because the forged IP will not respond afterwards. The server will remain in SYN_RECV state and try again. This will cause TCP waiting for connection queue resources to be exhausted and normal business cannot be carried out.

Shrew DDoS
----------------------------------------
Shrew DDoS uses TCP's retransmission mechanism to adjust the attack cycle to repeatedly trigger the RTO of the TCP protocol to achieve the attack effect. Its packets are sent at a fixed, maliciously selected slow time, a mode that limits TCP traffic to a small part of its ideal rate while transmitting at an average rate low enough to avoid detection.

Modern operating systems have made corresponding modifications to the TCP protocol so that it is not affected.

Ping Of Death
----------------------------------------
Under normal circumstances, there will be no ICMP packets greater than 65536 bytes, but packets support shard reorganization mechanism. In this way, ICMP packets greater than 65536 bytes can be sent and reorganized on the target host, which will eventually cause the target buffer to overflow and cause a denial of service attack.

Modern operating systems have checked this attack method so that it is not affected.

Challenge Collapsar (CC)
----------------------------------------
CC attack is a DoS attack targeting resources. Attackers usually use requests to consume server resources to achieve their goals.

There are many ways to attack CC. Common attacks can be achieved through a large number of expensive functions such as search pages and item display pages. Some HTTP servers can also implement attacks by uploading super large files and sending requests for large and complex parameters.

Slow attack
----------------------------------------
HTTP slow attack was officially disclosed by Wong Onn Chee and Tom Brennan at the 2012 OWASP Conference, using low-speed packets to consume server resources to achieve the purpose of denial of service.

Slow attacks are divided into three attack methods: Slow headers / Slow body / Slow read. Slow headers keep sending HTTP headers slowly, consuming server connections and memory resources. Slow body sends a Content-Length HTTP POST request, sending only a small amount of data at a time, keeping the connection alive. Slow reads the Response at a very low speed.

Based on service features
----------------------------------------
- Compression pack decompression
- Huge 0 bytes of compressed package
- Read the file
- Read unlimited files such as ``/dev/urandom``
- High frequency access to specific large file download links
- Restricted deserialization
- Deserialize huge arrays
- Regular analysis
- A huge backtracking expression

Common protection methods
----------------------------------------
- Fingerprint detection attack based on specific attacks, block/speed limit operation of corresponding traffic
- Model normal traffic and block/speed limit the identified abnormal traffic
- Comprehensive speed limiting strategy based on IP/port
- Block/speed limit operation based on geographical location

Reference link
----------------------------------------
-`Linux Academy of <https://linuxaCademy.com/howtoguides/posts/show/topic/13191-denial-of-service-dos>` _
- `slowhttptest <https://github.com/shekyan/slowhttptest>`_ Application Layer DoS attack simulator
- `Slowloris wiki <https://en.wikipedia.org/wiki/Slowloris_(computer_security)>`_
