denial of service attack
========================================

Introduction
----------------------------------------
DoS (Denial of Service) refers to denial of service, which is a network attack method commonly used to paralyze servers or networks.

In normal times, Distributed Denial of Service (DDoS) attacks are more commonly mentioned. This attack refers to using a sufficient number of puppet computers to generate a huge number of attack packets to carry out DDoS attacks on one or more targets on the network, exponentially increasing the power, thus exhausting the resources of the victim target and forcing the target to lose the ability to provide normal services.

UDP reflection
----------------------------------------
Reflection DDoS attacks based on UDP messages are a form of denial of service attacks. The attacker does not attack the target directly, but uses some open servers on the Internet to forge the address of the attacker and send a special UDP service-based request message to the server, causing several times the data of the request message to be sent to the attacked IP, thereby indirectly forming a DDoS attack on the latter.

Services commonly used in DoS attacks include:

- NTP
- DNS
- SSDP
- Memcached

Among them, DNS attacks mainly refer to DNS Request Flood, DNS Response Flood, fake source + real source DNS Query Flood, authoritative server attack and Local server attack.

TCP Flood
----------------------------------------
TCP Flood is an attack that exploits flaws in the TCP protocol. This method sends a large number of forged TCP SYN requests to the attacking server by forging IPs. After the attacked server responds with a handshake packet (SYN+ACK), because the forged IP will not respond to subsequent handshake packets, the server will remain in the SYN_RECV state and try again. This will cause the TCP waiting connection queue resources to be exhausted and normal services to be unable to proceed.

Shrew DDoS
----------------------------------------
Shrew DDoS takes advantage of TCP's retransmission mechanism and adjusts the attack cycle to repeatedly trigger the RTO of the TCP protocol to achieve the attack effect. Its packets are sent at a fixed, maliciously chosen slow time, a pattern that limits TCP traffic to a fraction of its ideal rate while transmitting at an average rate low enough to avoid detection.

Modern operating systems have made corresponding modifications to the TCP protocol so that it is not affected.

Ping Of Death
----------------------------------------
Under normal circumstances, there will be no ICMP packets larger than 65536 bytes, but the packets support the fragmentation and reassembly mechanism. In this way, ICMP packets larger than 65536 bytes can be sent and reassembled on the target host, which will eventually cause the target buffer to overflow and cause a denial of service attack.

Modern operating systems have checks for this attack style, making it unaffected.

Challenge Collapsar (CC)
----------------------------------------
A CC attack is a DoS attack targeting resources. Attackers usually use requests that consume server resources to achieve their goals.

There are many ways to attack CC. Common attacks can be achieved by accessing large amounts of search pages, item display pages and other expensive functions. Some HTTP servers can also implement attacks by uploading very large files and sending requests with large and complex parameters.

slow attack
----------------------------------------
The HTTP slow attack was officially disclosed by Wong Onn Chee and Tom Brennan at the OWASP conference in 2012. It uses low-speed packet sending to consume server resources to achieve the purpose of denial of service.

Slow attacks are divided into three attack methods: Slow headers / Slow body / Slow read. Slow headers continuously send HTTP headers slowly, consuming the server's connection and memory resources. Slow body sends an HTTP POST request with a large Content-Length, sending only a small amount of data each time to keep the connection alive. Slow read reads the Response at a very low speed.

Based on service characteristics
----------------------------------------
- Decompress the compressed package
    - Huge 0-byte compressed package
- read files
    - Read unlimited files such as ``/dev/urandom``
    - Highly access specific large file download links
- Restricted deserialization
    - Deserialize huge arrays
- Regular analysis
    - Expensive backtracking expression

Commonly used protection methods
----------------------------------------
- Detect attacks based on fingerprints of specific attacks, and block/limit the corresponding traffic
- Model normal traffic and block/limit speed on identified abnormal traffic
- Comprehensive rate limiting strategy based on IP/port
- Block/speed limit operations based on geographical location

Reference link
----------------------------------------
- `linux academy dos <https://linuxacademy.com/howtoguides/posts/show/topic/13191-denial-of-service-dos>`_
- `slowhttptest <https://github.com/shekyan/slowhttptest>`_ Application Layer DoS attack simulator
- `Slowloris wiki <https://en.wikipedia.org/wiki/Slowloris_(computer_security)>`_
