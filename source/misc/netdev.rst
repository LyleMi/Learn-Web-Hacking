Common network equipment
========================================

firewall
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A firewall refers to a protective barrier that is composed of software and hardware devices and is constructed on the interface between the internal network and the external network, and between the private network and the public network. It can achieve network security protection by monitoring, restricting, and changing the data flow across the firewall, and shielding the information, structure, and operating status of the network from the outside as much as possible.

Firewalls can be divided into network layer firewalls and application layer firewalls. Network layer firewalls make pass or fail decisions based on the source and destination addresses, applications, protocols, and ports of each IP packet. Application layer firewalls target special network application service protocols, namely data filtering protocols, and can analyze data packets and form relevant reports.

Main functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Filter data entering and leaving the network
- Prevent unsafe protocols and services
- Manage access behavior in and out of the network
- Record the information content passing through the firewall
- Detect and warn against network attacks
- Prevent external access to internal network information
- Provides centralized management of external connections

next generation firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It is mainly a high-performance firewall that comprehensively responds to application layer threats. It can achieve features such as intelligent active defense, application layer data leakage prevention, application layer insight and control, and threat protection.
The next-generation firewall integrates traditional firewall, IPS, application identification, content filtering and other functions in one device, which not only reduces the procurement investment of the overall network security system, but also reduces the deployment costs caused by multiple devices accessing the network. It also reduces the maintenance and management costs of managers through application identification and user management technologies.

IDS
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Intrusion detection collects and analyzes information from several key nodes in the network system to monitor whether there are violations of security policies or intrusions in the network. Intrusion detection systems usually contain three necessary functional components: information source, analysis engine and response component.

Information collection includes collecting the status and behavior of systems, networks, data and user activities. The information utilized by intrusion detection generally comes from three aspects: system and network log files, abnormal directory and file changes, and abnormal program execution.

The analysis engine analyzes the collected information about the status and behavior of systems, networks, data, and user activities through pattern matching, statistical analysis, and integrity analysis. The first two are used for real-time intrusion detection, and integrity analysis is used for post-event analysis.

Alarms and responses: Based on the nature and type of intrusion, corresponding alarms and responses are made.

Main types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
IDS can be divided into host-based intrusion detection system (HIDS) and network-based intrusion detection system (NIDS).

The host-based intrusion detection system is an early intrusion detection system structure, usually software-based and installed directly on the host that needs to be protected. The detection targets are mainly the host system and local users of the system. The detection principle is to discover suspicious events based on the audit data and system logs of the host.

The main advantages of this detection method are: more detailed information, lower false alarm rate, and flexible deployment. The main disadvantages of this method are: it will reduce the performance of the application system; it relies on the original log and monitoring capabilities of the server; it is expensive; it cannot monitor the network; it requires the installation of multiple detection systems for different systems.

Network-based intrusion detection method is currently a relatively mainstream monitoring method. This type of detection system requires a specialized detection equipment. The detection equipment is placed in a more important network segment and constantly monitors various data packets in the network segment, instead of only monitoring a single host. It performs characteristic analysis on every data packet or suspicious data packet on the monitored network. If the data packet matches certain rules built into the product, the intrusion detection system will issue an alarm or even directly cut off the network connection. Currently, most intrusion detection products are network-based.

The main advantages of this detection technology are: it can detect attacks from the network and illegal access that exceeds authorization; it does not need to change the configuration of hosts such as servers, and will not affect host performance; it has low risk; and it is simple to configure. Its main disadvantages are: high cost and limited detection range; a large amount of calculations, which affects system performance; a large amount of analysis of data flows, which affects system performance; it is difficult to process encrypted session processes; when the network flow rate is high, many packets may be lost, which may easily allow intruders to take advantage; encrypted packets cannot be detected; direct intrusions to the host cannot be detected.

IPS (Intrusion Prevention System)
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
An intrusion prevention system is a computer network security device that can monitor the network data transmission behavior of a network or network device, and can immediately interrupt, adjust or isolate some abnormal or harmful network data transmission behaviors.

Serially deployed firewalls can block low-level attacks, but are powerless against deep-level attacks at the application layer. The IDS deployed in the side channel can promptly discover deep attack behaviors that penetrate the firewall and serve as a useful supplement to the firewall, but it cannot block them in real time.

Therefore, IPS based on the linkage between IDS and firewalls emerged: discovered through IDS and blocked through firewalls. However, due to the lack of unified interface specifications so far, and the increasingly frequent "instant attacks" (attack effects can be achieved in one session, such as SQL injection, overflow attacks, etc.), the linkage between IDS and firewalls is not effective in practical applications.

Main types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It can be divided into feature-based IPS, anomaly-based IPS, policy-based IPS, and protocol analysis-based IPS.

Signature-based IPS is the most common approach among many IPS solutions. Add signatures to devices to identify today's most common attacks. Also known as pattern matching IPS. Signature libraries can be added, adapted and updated to respond to new attacks.

Anomaly-based IPS is also called profile-based IPS. Anomaly-based methods can use statistical anomaly detection and non-statistical anomaly detection.

Policy-based IPS is more concerned with executing the organization's security policy. An alarm is triggered if the detected activity violates the organization's security policy. IPS using this method needs to write security policies into the device.

Protocol analysis-based IPS is similar to signature-based methods. Most cases check for common signatures, but methods based on protocol analysis can do deeper packet inspection and be more flexible in finding certain types of attacks.

Security isolation gate
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The security isolation gatekeeper is an information security device that uses solid-state switch read-write media with multiple control functions to connect two independent network systems. Because there are no physical connections, logical connections, information transmission commands, information transmission protocols for communication between two independent network systems connected by a physically isolated gatekeeper, there is no packet forwarding based on the protocol, there is only a protocol-free "ferry" of data files, and there are only two commands for solid-state storage media, "read" and "write". Therefore, the physical isolation gatekeeper physically isolates and blocks all connections with potential attacks, making it impossible for attackers to invade, attack, or destroy, achieving true security.

Main functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Block direct physical connections to the network: The physically isolated gatekeeper can only be connected to one of the untrusted network and the trusted network at any time, but cannot be connected to both networks at the same time.

Block the logical connection of the network: The physical isolation gatekeeper does not depend on the operating system and does not support the TCP/IP protocol. The information exchange between the two networks must strip away the TCP/IP protocol, forward the original data through P2P non-TCP/IP connection, and complete data forwarding through "writing" and "reading" of the storage medium.

Security review: The physical isolation gatekeeper has a security review function, that is, before the network "writes" the original data to the physical isolation gatekeeper, it checks the security of the original data as needed to filter out possible virus codes and malicious attack codes.

The original data is non-hazardous: the original data forwarded by the physically isolated gatekeeper has no characteristics of attack or harmful to network security.

Management and control functions: Establish a complete log system.

Establish a data feature library as needed: During the application initialization phase, combined with the application requirements, the characteristics of the application data are extracted to form a user-specific data feature library, which serves as the basis for data verification during operation. When the user makes a request, the user's application data is extracted, the data features are extracted and compared with the original data feature library. Data requests that match the original feature library enter the request queue, and those that do not match are returned to the user to implement data filtering.

Provides the function of customizing security policies and transmission policies as needed: users can set their own data transmission policies, such as: transmission unit (data-based or task-based), transmission interval, transmission direction, transmission time, startup time, etc.

Supports scheduled/real-time file exchange; supports one-way/two-way file exchange; supports digital signatures, content filtering, virus checking and other functions.

VPN device
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Virtual private network refers to the technology of establishing a private network on a public network. It is called a virtual network mainly because the connection between any two nodes of the entire VPN network does not have the end-to-end physical link required by the traditional private network. Instead, it is a logical network built on the network platform provided by the public network service provider. User data is transmitted in the logical link.

Commonly used techniques
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MPLS VPN: It is an IP VPN based on MPLS technology. It applies MPLS (Multi-Protocol Label Switching) technology on network routing and switching equipment, simplifies the routing selection method of core routers, and uses label switching combined with traditional routing technology to implement an IP virtual private network (IP VPN). The advantage of MPLS is that it combines Layer 2 switching and Layer 3 routing technologies, and has excellent performance in solving major problems in IP networks such as VPN, service classification and traffic engineering. Therefore, MPLS VPN is increasingly favored by operators in solving enterprise interconnection and providing various new services, and has become an important means for IP network operators to provide value-added services. MPLS VPN can be divided into two-layer MPLS VPN (MPLS L2 VPN) and three-layer MPLS VPN (MPLS L3 VPN).

SSL VPN: It is a VPN technology based on HTTPS (SecureHTTP, secure HTTP, that is, the HTTP protocol that supports SSL) and works between the transport layer and the application layer. SSL VPN makes full use of the certificate-based identity authentication, data encryption and message integrity verification mechanisms provided by the SSL protocol to establish secure connections for communication between application layers. SSL VPN is widely used in web-based remote secure access, providing security guarantee for users to remotely access the company's internal network.

IPSecVPN is a VPN technology based on the IPSec protocol. The IPSec protocol provides tunnel security. IPSec is an end-to-end mechanism designed by IETF to ensure data security based on IP communications. It provides high-quality, interoperable, cryptography-based security guarantees for data transmitted on the Internet.

Security audit system
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The network security audit system provides effective behavior audit, content audit, behavior alarm, behavior control and related audit functions for Internet behavior. Provide effective supervision of the Internet from the management level to prevent and stop data leaks. Meet users' requirements for Internet behavior audit filing and security protection measures, and provide complete Internet access records to facilitate information tracking, system security management and risk prevention.

Reference link
----------------------------------------
- `Network security equipment <https://wenku.baidu.com/view/2b5540cca32d7375a517806a.html>`_
