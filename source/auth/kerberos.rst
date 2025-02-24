Kerberos
========================================

Introduction
----------------------------------------
The Kerberos protocol originated from the Athena project of the MIT Institute of Technology in the United States. It is based on the public-private key encryption system and provides two-way verification for distributed environments. It was adopted in RFC 1510. Kerberos is the default authentication protocol in Windows domain environments.

Simply put, Kerberos provides a single sign-on (SSO) method. Consider a scenario where there are different servers in a network, such as print servers, mail servers, and file servers. These servers have authentication requirements. It is natural that it is impossible to enable each server to implement an authentication system by itself, but to provide a central authentication server (AS) for these servers to use. In this way, any client can log in to all servers by just maintaining a password.

The Kerberos protocol is a Ticket-based system that has at least three roles in the Kerberos system: an authentication server (AS), a client (Client) and a normal server (Server).

The authentication server verifies the user and issues a TGT (Treasure Grant Ticket) for the user to request session tickets. The TGS (TGS) issues ST (Session Notes) for the network service based on the TGT issued to the customer.

In the Kerberos system, both the client and the server have a unique name, called Principal. At the same time, both the client and the server have their own passwords, and only their passwords are known to them and the authentication server AS.

Basic concepts
----------------------------------------
- Principal (safe individual)
- The certified individual has a name and password
- KDC (Key Distribution Center)
- Network services that provide tickets and temporary session keys
- Ticket
- A record that users can use to prove their identity to the server, including the user's identity, session key, timestamp, and some other information. Most of the information in the Ticket is encrypted, and the key is the server's key
- Authenticator
- A record containing some recently generated information that requires a session key shared between the user and the server
- Credentials
- A ticket plus a secret session key
- Authentication Server (AS)
- Authenticated users with long-term key
- AS gives users ticket granting ticket and short-term key
- Certification Service
- Ticket Granting Server (TGS)
- Authenticated users with short-term key and Ticket Granting Ticket
- TGS issues tickets to users to access other servers
- Authorization and access control services

Simplified certification process
----------------------------------------
1. The client initiates a request to the server, and the request content is: the client's principal, the server's principal
2. After AS receives the request, it randomly generates a password Kc, s(session key), and generates the following two tickets and returns them to the client.
1. The ticket to the client is encrypted with the client's password, and the content is a random password, session, server_principal
2. Encrypt the ticket to the server side with the server's password, and the content is a random password, session, client_principal
3. After the client gets the two bills in the second step, he first uses his own password to unbox the bills, obtain Kc and s, and then generates an Authenticator, which mainly includes the verification codes of the current time and Ts, c, and Encrypted with SessionKey Kc,s. Then the client sends Authenticator and the tickets to the server to the server at the same time
4. The server first uses its own password to unbox the invoice, get the SessionKey Kc,s, and then unbox the Authenticator with Kc,s, and do the following check
1. Check whether the timestamp in Authenticator is within 5 minutes of the current time, and check whether the timestamp appears for the first time. If this timestamp is not the first time it appears, it means that someone intercepted the content sent by the client and carried out a Replay attack.
2. Check if checksum is correct
3. If all are correct, the client will pass the authentication
5. The server segment can optionally reply a message to the client to complete two-way authentication, with the content encrypted time stamps with session key
6. The client verifies the server by unpacking the message and comparing whether the sent back timestamp is consistent with the timestamp sent by itself.

Complete certification process
----------------------------------------
The process introduced above has been able to complete mutual authentication between the client and the server. However, what is more inconvenient is that the client requires the client to enter its own password every time he or she authenticates.

Therefore, in the Kerberos system, a new role was introduced called: Ticket Granting Service (TGS - Ticket Granting Service), which is similar to an ordinary server, except that the service it provides is distributed to clients and other servers. Certified bills.

In this way, there are four roles in the Kerberos system: authentication server (AS), client (Client), ordinary server (Server) and ticket authorization service (TGS). In this way, the authentication process for the client to communicate with the server for the first time is divided into the following 6 steps:

1. The client initiates a request to the AS, and the request content is: the client's principal, the bill authorization server's rincipal
2. After the AS receives the request, it randomly generates a password Kc, s(session key), and generates the following two tickets to return to the client:
1. The ticket to the client is encrypted with the client's password, and the content is a random password, session, tgs_principal
2. The ticket to tgs is encrypted with the password of tgs, and the content is a random password, session, client_principal
3. After the client gets the two bills in the second step, he first uses his own password to unbox the bills, obtain Kc and s, and then generates an Authenticator, which mainly includes the verification codes of the current time and Ts, c, and Encrypted with SessionKey Kc,s. Then the client initiates a request to tgs, including:
1. Authenticator
2. Send the ticket to tgs to the server at the same time
3. server_principal
4. TGS first unboxes the invoice with its own password, get the SessionKey Kc,s, and then unboxes the Authenticator with Kc,s, and do the following check
1. Check whether the timestamp in Authenticator is within 5 minutes of the current time, and check whether the timestamp appears for the first time. If this timestamp is not the first time it appears, it means that someone intercepted the content sent by the client and carried out a Replay attack.
2. Check if checksum is correct
3. If all are correct, the client will pass the authentication
5. tgs generates a session key to assemble two tickets to the client
1. The tickets encrypted with the session key of the client and tgs, including the newly generated session key and server_principal
2. Encrypted tickets with the server's password, including the newly generated session key and client principal
6. After the client receives two tickets, it unties its own, then generates an Authenticator and sends a request to the server, including
1. Authenticator
2. Tickets to the server
7. After the server receives the request, it uses its own password to unbox the invoice and gets the session key, and then unboxes the authenticator with the session key to verify it for no reason.
8. The server can choose to return a time stamp encrypted with the session key to complete two-way verification.
9. The client verifies the server by unpacking the message and comparing whether the sent back timestamp is consistent with the timestamp sent by itself.

Pros and cons
----------------------------------------

advantage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Passwords are not easy to be escaped
- Password not transmitted online
- Password guessing is more difficult
- It is difficult to use after the bill is stolen because it needs to be used with the authentication header

shortcoming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Lack of revocation mechanism
- Introduced complex key management
- Requires clock synchronization
- Restricted stretchability

Reference link
----------------------------------------

specification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 1510 The Kerberos Network Authentication Service <https://tools.ietf.org/html/rfc1510>`_
- `Detailed explanation of Kerberos certification process <https://blog.csdn.net/jewes/article/details/20792021>`_

attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Delegate to the Top: Abusing Kerberos for arbitrary impersonations and RCE <https://www.blackhat.com/docs/asia-17/materials/asia-17-Hart-Delegate-To-The-Top-Abusing-Kerberos-For-Arbitrary-Impersonations-And-RCE-wp.pdf>`_
- `Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94?redirectedfrom=MSDN>`_
- `Kerberos Technical Supplement for Windows <https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff649429(v=pandp.10)>`_
- `Cracking Kerberos TGS Tickets Using Kerberoast – Exploiting Kerberos to Compromise the Active Directory Domain <https://adsecurity.org/?p=2293>`_
