IPsec
========================================

Introduction
----------------------------------------
IPsec (IP Security) is a layer three-channel encryption protocol formulated by the IETF. It provides high-quality, interoperable, and cryptographic-based security assurance for data transmitted on the Internet. Specific communication parties provide the following security services through encryption and data source authentication at the IP layer:

- Confidentiality
- The IPsec sender encrypts the packet before transmitting it over the network.
- Data Integrity
- The IPsec receiver authenticates the packets sent by the sender to ensure that the data is not tampered with during transmission.
- Data Authentication
- IPsec can authenticate whether the sending end that sends IPsec packets is legal.
- Anti-Replay
- The IPsec receiver can detect and reject outdated or duplicate messages.

advantage
----------------------------------------
IPsec has the following advantages:

- Supports IKE (Internet Key Exchange), which can realize the automatic key negotiation function, reducing the overhead of key negotiation. The SA services can be established and maintained through IKE, which simplifies the use and management of IPsec.
- All application systems and services that use IP protocol for data transmission can use IPsec without any modification to these application systems and services themselves.
- Encryption of data is in units of data packets, not in units of the entire data stream, which is not only flexible but also helps to further improve the security of IP packets and can effectively prevent network attacks.

constitute
----------------------------------------
IPsec consists of four parts:

- Internet Key Exchange Protocol (Internet Key Exchange Protocol) responsible for key management
- Security Associations (Security Associations) that connects a security service to the communication flow that uses the service
- Directly operate packet authentication header protocol AH (IP Authentication Header) and security payload protocol ESP (IP Encapsulating Security Payload)
- Several algorithms for encryption and authentication

Security Association (SA)
----------------------------------------
IPsec provides secure communication between two endpoints, which are called IPsec peers.

SA is the basis of IPsec and the essence of IPsec. SA is a convention for certain elements between communication peers, such as which protocol is used (AH, ESP or a combination of both), the protocol's encapsulation mode (transmission mode and tunnel mode), encryption algorithms (DES, 3DES, and AES), shared keys that protect data in a specific stream, and the lifetime of the key. There are two ways to establish SA: manual configuration and IKE automatic negotiation.

SA is unidirectional. In bidirectional communication between two peers, at least two SAs are required to protect data flows in both directions separately. Meanwhile, if two peers want to use AH and ESP simultaneously for secure communication, each peer will build a separate SA for each protocol.

SA is uniquely identified by a triple, which includes SPI (Security Parameter Index), destination IP address, and security protocol number (AH or ESP).

SPI is a 32-bit value used to uniquely identify SA, which is transmitted in AH and ESP headers. When manually configuring SA, you need to manually specify the SPI value. When SA is generated using IKE negotiation, the SPI is generated randomly.

IKE
----------------------------------------
IKE (RFC2407, RFC2408, RFC2409) is a hybrid protocol, consisting of the Internet Security Association and Key Management Protocol (ISAKMP) and two key exchange protocols OAKLEY and SKEME. IKE is created in the framework defined by ISAKMP, using OAKLEY's key exchange mode and SKEME's sharing and key update technology, and also defines its own two key exchange methods.

IKE uses two stages of ISAKMP:

In the first stage, we negotiate to create a communication channel (IKE SA) and verify the channel to provide confidentiality, message integrity and message source verification services for further IKE communication between both parties;
In the second stage, an IPsec SA is established (called Child SA in V2).
