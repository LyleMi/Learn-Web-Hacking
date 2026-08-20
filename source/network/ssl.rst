SSL/TLS
========================================

Introduction
----------------------------------------
The full name of SSL is Secure Sockets Layer. It was designed by Netscape in 1994 and is mainly used as a secure transmission protocol for the Web. It aims to provide confidentiality, authentication and data integrity guarantees for network communications. Today, SSL has become the industry standard for secure communications on the Internet.

The first few versions of SSL (SSL 1.0, SSL2.0, SSL 3.0) were designed and maintained by Netscape. Starting from version 3.1, the SSL protocol was officially taken over by the Internet Engineering Task Force (IETF) and renamed TLS (Transport Layer Security). So far, there are several versions of TLS 1.0, TLS1.1, TLS1.2, and TLS1.3.

As the name TLS says, the SSL/TLS protocol only ensures transport layer security. At the same time, due to the characteristics of the protocol itself (digital certificate mechanism), SSL/TLS cannot be used to protect multi-hop end-to-end communications, but can only protect point-to-point communications.

The security goals that the SSL/TLS protocol can provide mainly include the following:

- Authentication
- Use digital certificates to authenticate server and client identities to prevent identity forgery
- Confidentiality
- Protect against third-party eavesdropping with encryption
- Completeness
- Ensure data integrity and prevent message tampering with the help of Message Authentication Code (MAC)
- Replay protection
- Prevent replay attacks by using implicit sequence numbers

In order to achieve these security goals, the SSL/TLS protocol is designed as a two-phase protocol, divided into a handshake phase and an application phase:

The handshake phase is also called the negotiation phase. In this phase, the client and the server authenticate each other's identity (relying on the PKI system and using digital certificates for identity authentication), and negotiate the security parameters, cipher suites, and MasterSecret used in communication. All keys used for subsequent communications are generated through MasterSecret.
After the handshake phase is completed, the application phase is entered. In the application phase, the communicating parties use the keys negotiated in the handshake phase for secure communication.

protocol
----------------------------------------
TLS contains several sub-protocols, the more commonly used ones are the recording protocol, the alarm protocol, the handshake protocol, the change password specification protocol, etc.

record agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Record Protocol specifies the basic unit record for TLS data transmission and reception.

alarm protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Alert Protocol is used to prompt errors in the protocol interaction process.

handshake agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Handshake Protocol is the most complex sub-protocol in TLS. During the handshake process, the TLS version number, random number, cipher suite and other information are negotiated, and then certificate and key parameters are exchanged. Finally, the two parties negotiate to obtain the session key, which is used in the subsequent hybrid encryption system.

Change Password Specification Agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Change Cipher Spec Protocol is a "notification" that tells the other party that all subsequent data will be protected by encryption.

interactive process
----------------------------------------

Client Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Client Hello is sent by the client and includes a Unix timestamp (GMT Unix Time) of the client, some random bytes (Random Bytes), and the type of algorithm accepted by the client (Cipher Suites).

Server Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Server Hello is sent by the server and includes the algorithm type, GMT Unix Time and Random Bytes supported by the server.

Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the server or client, the sender will send its digital certificate to the receiver, and the receiver will verify the certificate. If it fails, the receiver will interrupt the handshake process. Generally follows the Client/Server Hello message.

Server Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the server, it transmits its public key parameters to the client, usually in the same TCP message as Server Hello and Certificate.

Server Hello Done
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the server, usually in a TCP message with Server Hello, Certificate and Server Key Exchange.

Client Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The client sends, sends its own public key parameters to the server, and negotiates the key with the server.

Change Cipher Spec
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the client or server, followed by Key Exchange, it means that it has generated a new key and notified the other party that it will change the key in the future and use the new key for communication.

Encrypted Handshake Message
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the client or server, followed by Key Exchange. For testing, one party uses its newly generated key to encrypt a fixed message and sends it to the other party. If the key negotiation is correct, the other party can decrypt it correctly.

New Session Ticket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sent by the server, indicating the initiation of a session. Within a period of time (before the timeout arrives), both parties communicate with the key just exchanged. From then on, encrypted communication officially began.

Application Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Application layer data encrypted using keys negotiated by the key exchange protocol.

Encrypted Alert
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sending by the client or server means that encrypted communication needs to be interrupted for some reason, and the other party is warned not to send sensitive data again.

Version update content
----------------------------------------

TLS 1.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Introduced PSK as a new key agreement mechanism
- Supports 0-RTT mode, which saves round-trip time when establishing a connection at the expense of reduced security
- All handshake messages after ServerHello are encrypted, and the visible plain text is reduced.
- Compression of encrypted messages is no longer allowed, and both parties are no longer allowed to initiate renegotiation.
- DSA certificates are no longer allowed in TLS 1.3
- Removed insecure cryptographic algorithms
- RSA key transport - forward security not supported
- CBC mode cipher - vulnerable to BEAST and Lucky 13 attacks
- RC4 stream cipher - not secure for use in HTTPS
- SHA-1 hash function - it is recommended to replace it with SHA-2
- Arbitrary Diffie-Hellman Group - CVE-2016-0701 vulnerability
- Output password - Vulnerable to FREAK and LogJam attacks

sub-protocol
----------------------------------------
The SSL/TLS protocol has a highly modular architecture and is divided into many sub-protocols, mainly:

- Handshake protocol
- Including negotiation of security parameters and cipher suites, server identity authentication (client identity authentication is optional), and key exchange
- ChangeCipherSpec protocol
- A message indicating that the handshake protocol has been completed
- Alert protocol
- Error reminders for some exceptions in the handshake protocol are divided into two levels: fatal and warning. Fatal type errors will directly interrupt the SSL link, while warning level errors can still continue the SSL link, but will give an error warning.
- Record protocol
- Including message segmentation, compression, message authentication and integrity protection, encryption, etc.

Reference link
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 2246 The TLS Protocol Version 1.0 <https://tools.ietf.org/html/rfc2246>`_
- `RFC 4346 The Transport Layer Security (TLS) Protocol Version 1.1 <https://tools.ietf.org/html/rfc4346>`_
- `RFC 5246 The Transport Layer Security (TLS) Protocol Version 1.2 <https://tools.ietf.org/html/rfc5246>`_
- `RFC 6101 The Secure Sockets Layer (SSL) Protocol Version 3.0 <https://tools.ietf.org/html/rfc6101>`_
- `RFC 6176 Prohibiting Secure Sockets Layer (SSL) Version 2.0 <https://tools.ietf.org/html/rfc6176>`_
- `RFC 7568 Deprecating Secure Sockets Layer Version 3.0 <https://tools.ietf.org/html/rfc7568>`_
- `RFC 8446 The Transport Layer Security (TLS) Protocol Version 1.3 <https://tools.ietf.org/html/rfc8446>`_

Document
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Wikipedia Transport Layer Security <https://en.wikipedia.org/wiki/Transport_Layer_Security>`_
