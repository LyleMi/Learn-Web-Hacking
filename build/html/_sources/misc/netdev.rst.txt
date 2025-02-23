Common network equipment
========================================

Firewall
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A firewall refers to a protective barrier composed of a combination of software and hardware devices and constructed on the interface between the internal network and the external network, and between the dedicated network and the public network. It can achieve network security protection by monitoring, limiting and changing the data flow across the firewall, and blocking the information, structure and health status inside the network as much as possible.

Firewalls can be divided into network layer firewalls and application layer firewalls. The network layer firewall makes a judgment on whether it passes or not based on the source and destination addresses, applications, protocols, and ports of each IP packet. The application layer firewall targets a special network application service protocol, namely a data filtering protocol, and can analyze data packets and form related reports.

Main functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Filter data from in and out of the network
- Prevent unsafe protocols and services
- Manage access behaviors in and out of the network
- Record information through the firewall
- Detect and alert cyber attacks
- Prevent external access to internal network information
- Provide centralized management of external connections

Next Generation Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It is mainly a high-performance firewall that fully deals with application-layer threats. It can achieve intelligent and active defense, application-level data leakage prevention, application-level insight and control, threat protection and other features.
The next-generation firewall integrates traditional firewalls, IPS, application identification, content filtering and other functions into one device, which not only reduces the procurement investment of the overall network security system, but also reduces the deployment costs caused by accessing multiple devices to the network. The maintenance and management costs of managers are reduced through technologies such as application identification and user management.

IDS
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Intrusion detection means collecting and analyzing information from several key nodes in the network system to monitor whether there are any violations of security policies or whether there are any intrusions in the network. An intrusion detection system usually contains 3 necessary functional components: information source, analysis engine and response component.

Information collection includes the status and behavior of collecting systems, networks, data and user activities. The information used by intrusion detection generally comes from three aspects: system and network log files, abnormal directories and file changes, and abnormal program execution.

The analysis engine analyzes the collected information about the status and behavior of the system, network, data, and user activities through three means: pattern matching, statistical analysis and integrity analysis. The first two are used for real-time intrusion detection, and integrity analysis is used for post hoc analysis.

Alarms and responses make corresponding alarms and responses based on the nature and type of intrusion.

Main types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
IDS can be divided into host-based intrusion detection system (HIDS) and network-based intrusion detection system (NIDS).

The host-based intrusion detection system is an early intrusion detection system structure, usually software-based, and is directly installed on the host that needs protection. The target of its detection is mainly the host system and the system local users. The detection principle is to discover suspicious events based on the host's audit data and system log.

The main advantages of this detection method are: more detailed information, low false alarm rate, and flexible deployment. The main disadvantages of this method are: it will reduce the performance of the application system; it depends on the server's original logs and monitoring capabilities; it is expensive; it cannot monitor the network; and multiple detection systems for different systems need to be installed.

Network-based intrusion detection is currently a relatively mainstream monitoring method. This type of detection system requires a special detection equipment. The detection equipment is placed in a relatively important network segment and constantly monitors various data packets in the network segment, instead of monitoring only a single host. It performs characteristic analysis of every data packet or suspicious data packet on the monitored network. If the data packet matches certain rules built into the product, the intrusion detection system will issue an alarm and even directly cut off the network connection. Currently, most intrusion detection products are network-based.

The main advantages of this detection technology are: being able to detect attacks from the network and illegal access beyond authorization; no need to change the configuration of hosts such as servers and will not affect host performance; low risk; simple configuration. The main disadvantages are: high cost and limited detection range; large amount of calculations affects system performance; large amount of data flow analyzes, affects system performance; difficult to process encrypted session processes; many packets may be lost when the network flow rate is high, which is easy to make Intruders have the opportunity to take advantage of it; they cannot detect encrypted packets; they cannot detect direct intrusion into the host.

IPS (Intrusion Prevention System)
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
An intrusion prevention system is a computer network security device that can monitor the network data transmission behavior of network or network equipment. It can instantly interrupt, adjust or isolate some abnormal or harmful network data transmission behaviors.

A serially deployed firewall can intercept low-level attack behavior, but it can do nothing to the deep-level attack behavior of the application layer. Bypass deployment IDS can promptly detect deep attacks that penetrate the firewall, which is a useful supplement to the firewall, but cannot be blocked in real time.

Therefore, IPS based on IDS and firewall linkage has emerged: IDS is discovered and blocked through firewall. However, since there is no unified interface specification so far, coupled with the increasingly frequent "instant attacks" (one session can achieve attack effects, such as SQL injection, overflow attacks, etc.), the effect of linking IDS and firewalls in actual applications is achieved. Not significant.

Main types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It can be divided into feature-based IPS, exception-based IPS, policy-based IPS, and protocol-based IPS.

Feature-based IPS is the most commonly used method in many IPS solutions. Adding features to the device can identify the most common attacks currently available. Also known as pattern matching IPS. The feature library can be added, adjusted, and updated to deal with new attacks.

Exception-based IPS is also called industry-based IPS. Anomaly-based methods can use statistical anomaly detection and non-statistic anomaly detection.

Policy-based IPS is more concerned with whether to implement an organization's security policy. An alarm will be triggered if the detected activity violates the organization's security policy. Using this method, security policies should be written into the device.

Protocol-based analysis IPS is similar to feature-based approaches. Most cases check common features, but protocol analysis-based methods can perform more in-depth packet inspections and allow more flexibility in detecting certain types of attacks.

Safety isolation gate
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The safety isolation gate is an information security device that connects two independent network systems using solid-state switch read and write media with multiple control functions. Since there is no physical connection, logical connection, information transmission command, and information transmission protocol for communication between the two independent network systems connected to the physical isolation gate, there is no communication packet forwarding based on the protocol, and there is only the data file without a protocol. ferry", and there are only two commands for solid-state storage media, "read" and "write". Therefore, the physical isolation network gate physically isolates and blocks all connections with potential attacks, making it impossible for attackers to invade, attack, and destroy, achieving true security.

Main functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Block the direct physical connection of the network: The physical isolation gate can only connect to one of the untrusted networks and trusted networks at any time, and cannot connect to both networks at the same time.

Block the logical connection of the network: The physical isolation gate does not rely on the operating system and does not support the TCP/IP protocol. The information exchange between the two networks must strip the TCP/IP protocol, and the original data must be forwarded through P2P's non-TCP/IP connection method, and the data is forwarded through "write" and "read out" of the storage medium.

Security review: The physical isolation network gate has a security review function, that is, before the network "writes" the original data to the physical isolation network gate, the security of the original data is checked as needed, and filters out possible virus codes and malicious attack codes. .

The original data is not harmful: the raw data forwarded by the physical isolation gate does not have the characteristics of attack or harmful to network security.

Management and control functions: establish a complete logging system.

Establish a data feature database according to needs: During the application initialization stage, in combination with application requirements, the characteristics of the application data are extracted to form a user-specific data feature database as the basis for data verification during operation. When the user requests, the user's application data is extracted, the data characteristics are extracted and the original data feature database is compared. The data requests that meet the original feature database enter the request queue, and those that do not meet are returned to the user to achieve data filtering.

Provide the functions of customizing security policies and transmission policies as needed: users can set the data transmission strategy themselves, such as: transmission unit (based on data or task), transmission interval, transmission direction, transmission time, startup time, etc.

Supports timed/real-time file exchange; supports one-way/two-way file exchange; supports digital signature, content filtering, virus inspection and other functions.

VPN devices
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A virtual private network refers to the technology of establishing a private network on a public network. The reason why it is called a virtual network is mainly because the connection between any two nodes of the entire VPN network does not have the end-to-end physical link required by traditional private networks, but is built on the network platform provided by public network service providers. on the logical network, user data is transmitted in the logical link.

Commonly used technologies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MPLS VPN: It is an IP VPN based on MPLS technology. It uses MPLS (multi-protocol tag switching) technology on network routing and switching devices to simplify the routing method of core routers and use tag switching to combine traditional routing technology to implement IP Virtual Private Network (IP VPN). The advantage of MPLS is that it combines layer 2 switching and layer 3 routing technology, which has excellent performance in solving major problems in IP networks such as VPN, service classification and traffic engineering. Therefore, MPLS VPN is increasingly favored by operators in solving enterprise interconnection and providing various new services, and has become an important means for IP network operators to provide value-added services. MPLS VPN can be divided into layer two MPLS VPN (i.e. MPLS L2 VPN) and layer three MPLS VPN (i.e. MPLS L3 VPN).

SSL VPN: It is a VPN technology based on HTTPS (SecureHTTP, secure HTTP, that is, HTTP protocol that supports SSL), which works between the transport layer and the application layer. SSL VPN makes full use of the certificate-based identity authentication, data encryption and message integrity verification mechanisms provided by the SSL protocol, and can establish a secure connection for communication between the application layer. SSL VPN is widely used in remote secure access based on the web, providing security guarantees for users to remotely access the company's internal network.

IPSecVPN is a VPN technology based on the IPSec protocol, and the IPSec protocol provides tunnel security. IPSec is an end-to-end mechanism designed by the IETF to ensure data security based on IP communications. It provides high-quality, interoperable, cryptographic-based security assurance for data transmitted on the Internet.

Security audit system
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The network security audit system provides effective behavioral audit, content audit, behavioral alarm, behavioral control and related audit functions for Internet behavior. Provide effective supervision of the Internet from the management level to prevent and stop data leakage. Meet users' requirements for Internet behavior audit filing and security protection measures, and provide complete Internet access records to facilitate information tracking, system security management and risk prevention.

Reference link
----------------------------------------
- `Cybersecurity Equipment <https://wenku.baidu.com/view/2b5540cca32d7375a517806a.html>`_
