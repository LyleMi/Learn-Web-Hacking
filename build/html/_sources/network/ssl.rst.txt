SSL/TLS
========================================

Introduction
----------------------------------------
The full name of SSL is Secure Sockets Layer, a secure socket layer. It was designed by Netscape in 1994 and is mainly used for secure transmission protocols for the Web. The purpose is to provide confidentiality, authentication and data for network communication. Integrity guarantee. Today, SSL has become the industrial standard for confidential communications in the Internet.

The initial several versions of SSL (SSL 1.0, SSL2.0, SSL 3.0) were designed and maintained by Netscape. Starting from version 3.1, the SSL protocol was officially taken over by the Internet Engineering Task Team (IETF) and was renamed TLS (Transport Layer). Security), TLS 1.0, TLS 1.1, TLS 1.2, and TLS 1.3 have been developed to date.

As the TLS name says, the SSL/TLS protocol only guarantees the security of the transport layer. At the same time, due to the protocol's own characteristics (digital certificate mechanism), SSL/TLS cannot be used to protect multi-hop end-to-end communication, but can only protect point-to-point communication.

The security goals that the SSL/TLS protocol can provide mainly include the following:

- Certification
- Use digital certificates to authenticate server-end and client identities to prevent identity forgery
- Confidentiality
- Prevent third-party eavesdropping with encryption
- Integrity
- Use message authentication code (MAC) to ensure data integrity and prevent message tampering
- Replay protection
- Prevent replay attacks by using implicit serial numbers

To achieve these security goals, the SSL/TLS protocol is designed as a two-stage protocol divided into a handshake phase and an application phase:

The handshake phase is also called the negotiation phase. In this phase, the client and server will authenticate the other party's identity (relying on the PKI system, using digital certificates for identity authentication), and negotiate security parameters, cipher suites and MasterSecret used in communication. All keys used for subsequent communications are generated via MasterSecret.
After the handshake phase is completed, enter the application phase. During the application phase, the communication parties use the keys negotiated during the handshake phase to conduct secure communication.

protocol
----------------------------------------
TLS contains several sub-protocols, and the most commonly used ones include record protocol, alarm protocol, handshake protocol, password change protocol, etc.

Recording agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Record Protocol specifies the basic unit record of TLS data transmission and reception.

Alarm Protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Alert Protocol is used to prompt errors in the protocol interaction process.

Handshake Agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Handshake Protocol is the most complex sub-protocol in TLS. During the handshake process, the TLS version number, random number, cipher suite and other information are negotiated, and then the certificate and key parameters are exchanged. Finally, the two parties negotiate to obtain the session key, which is used for Subsequent hybrid encryption system.

Change password specification protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Change Cipher Spec Protocol is a "notification" that tells the other party that subsequent data will be protected by encryption.

Interaction process
----------------------------------------

Client Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Client Hello is sent by the client, and the content includes a Unix timestamp (GMT Unix Time) of the client, some random bytes (Random Bytes), and also includes the algorithm type (Cipher Suites) accepted by the client.

Server Hello
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Server Hello is sent by the server, including the algorithm types supported by the server, GMT Unix Time, and Random Bytes.

Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Send it by the server or client. The sender will send its digital certificate to the receiver, and the receiver will perform certificate verification. If it fails, the receiver will interrupt the handshake process. Generally follows the Client/Server Hello message.

Server Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Send it by the server and transmit its own public key parameters to the client. It is generally in the same TCP message as Server Hello and Certificate.

Server Hello Done
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The server sends it in a TCP message, which is generally in the same TCP message as Server Hello, Certificate and Server Key Exchange.

Client Key Exchange
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The client sends it, sends its own public key parameters to the server, and negotiates the key with the server.

Change Cipher Spec
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The client or server sends it, followed by Key Exchange, represents that it has generated a new key, notifying the other party that it will change the key in the future and use the new key to communicate.

Encrypted Handshake Message
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Send by the client or server, followed by Key Exchange. For testing, one party uses its newly generated key to encrypt a fixed message and sends it to the other party. If the key negotiation is correct, the other party can decrypt it correctly.

New Session Ticket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The server sends it, indicating that the session is initiated. Within a period of time (before the timeout time arrives), both parties communicate with the keys they just exchanged. From then on, encrypted communication officially began.

Application Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The application layer data encrypted using the key exchange protocol negotiated.

Encrypted Alert
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sending by the client or server means that encrypted communication needs to be interrupted for some reason, warning the other party not to send sensitive data again.

Version update content
----------------------------------------

TLS 1.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Introduced PSK as a new key negotiation mechanism
- Supports 0-RTT mode, saving round trip time when establishing a connection at the cost of reduced security
- All handshake messages after ServerHello are encrypted, and the plain text is reduced
- No longer allowed to compress encrypted packets, no longer allowed both parties to initiate renegotiation
- DSA certificates are no longer allowed in TLS 1.3
- Delete unsafe password algorithm
- RSA key transmission - forward security is not supported
- CBC Mode Password - Vulnerable to BEAST and Lucky 13 Attacks
- RC4 Streaming Password - Not safe to use in HTTPS
- SHA-1 hash function - SHA-2 is recommended to replace it
- Any Diffie-Hellman Group - CVE-2016-0701 Vulnerability
- Output password - vulnerable to FREAK and LogJam attacks

Sub-Agreement
----------------------------------------
The SSL/TLS protocol has a highly modular architecture, divided into many subprotocols, mainly:

- Handshake Agreement
- Including negotiated security parameters and password suite, server identity authentication (optional client identity authentication), key exchange
- ChangeCipherSpec protocol
- A message indicates that the handshake agreement has been completed
- Alert Agreement
- Some abnormal error reminders in the handshake protocol are divided into two levels: fatal and warning. Fatal type errors will directly interrupt the SSL link, while warning level error SSL links can still continue, but will give an error warning.
- Record protocol
- Including segmentation, compression, message authentication and integrity protection, encryption, etc.

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
