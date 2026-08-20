IPsec
========================================

Introduction
----------------------------------------
IPsec (IP Security) is a three-layer tunnel encryption protocol developed by IETF. It provides high-quality, interoperable, cryptography-based security guarantee for data transmitted on the Internet. The following security services are provided between specific communicating parties at the IP layer through encryption and data source authentication:

- Data confidentiality (Confidentiality)
- The IPsec sender encrypts the packet before transmitting it over the network.
-Data Integrity
- The IPsec receiver authenticates the packets sent by the sender to ensure that the data has not been tampered with during transmission.
- Data source authentication (Data Authentication)
- IPsec can authenticate the sending end of the IPsec message at the receiving end whether it is legal.
- Anti-Replay
- IPsec receivers can detect and reject outdated or duplicate messages.

advantage
----------------------------------------
IPsec has the following advantages:

- Supports IKE (Internet Key Exchange, Internet Key Exchange), which can realize the automatic negotiation function of keys and reduce the cost of key negotiation. SA services can be established and maintained through IKE, simplifying the use and management of IPsec.
- All application systems and services that use the IP protocol for data transmission can use IPsec without making any modifications to these application systems and services themselves.
- The encryption of data is based on data packets instead of the entire data flow. This is not only flexible but also helps to further improve the security of IP data packets and can effectively prevent network attacks.

constitute
----------------------------------------
IPsec consists of four parts:

- Internet Key Exchange Protocol IKE (Internet Key Exchange Protocol) responsible for key management
- Security Associations (SA) responsible for linking security services with communication flows that use the service
- Directly operate the authentication header protocol AH (IP Authentication Header) and security payload protocol ESP (IP Encapsulating Security Payload) of the data packet
- Several algorithms for encryption and authentication

Security Association (SA)
----------------------------------------
IPsec provides secure communication between two endpoints, which are called IPsec peers.

SA is the foundation and essence of IPsec. SA is an agreement between communication peers on certain elements, such as which protocol to use (AH, ESP, or a combination of both), the encapsulation mode of the protocol (transport mode and tunnel mode), encryption algorithm (DES, 3DES, and AES), the shared key to protect data in a specific stream, and the life cycle of the key. There are two ways to establish SA: manual configuration and IKE automatic negotiation.

SA is one-way. Bidirectional communication between two peers requires at least two SAs to securely protect data flows in both directions. At the same time, if two peers want to use both AH and ESP for secure communication, each peer will build an independent SA for each protocol.

SA is uniquely identified by a triplet, which includes SPI (Security Parameter Index), destination IP address, and security protocol number (AH or ESP).

SPI is a 32-bit value used to uniquely identify the SA, which is transmitted in the AH and ESP headers. When manually configuring SA, you need to manually specify the SPI value. When using IKE negotiation to generate SA, SPI will be generated randomly.

IKE
----------------------------------------
IKE (RFC2407, RFC2408, RFC2409) is a hybrid protocol consisting of Internet Security Association and Key Management Protocol (ISAKMP) and two key exchange protocols OAKLEY and SKEME. IKE is built on the framework defined by ISAKMP, follows OAKLEY's key exchange mode and SKEME's sharing and key update technology, and also defines its own two key exchange methods.

IKE uses two stages of ISAKMP:

In the first stage, negotiate to create a communication channel (IKE SA) and verify the channel to provide confidentiality, message integrity and message source verification services for further IKE communication between both parties;
In the second phase, the established IKE SA is used to establish an IPsec SA (called Child SA in V2).
