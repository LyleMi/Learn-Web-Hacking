Kerberos
========================================

Introduction
----------------------------------------
The Kerberos protocol originated from the Athena project of the Massachusetts Institute of Technology in the United States. It is based on the public and private key encryption system and provides two-way authentication for distributed environments. It was adopted in RFC 1510. Kerberos is the default authentication protocol in the Windows domain environment.

Simply put, Kerberos provides a Single Sign-On (SSO) method. Consider a scenario where there are different servers in a network, such as a print server, a mail server, and a file server. These servers all have authentication requirements. Naturally, it is impossible for each server to implement its own authentication system. Instead, a central authentication server (AS) is provided for use by these servers. In this way, any client only needs to maintain one password to log in to all servers.

The Kerberos protocol is a ticket-based system. There are at least three roles in the Kerberos system: authentication server (AS), client (Client) and ordinary server (Server).

The authentication server authenticates the user and issues a TGT (Ticket Granting Ticket) that the user uses to request a session ticket. The Ticket Granting Service (TGS) issues ST (session tickets) for network services based on the TGT issued to the client.

In the Kerberos system, both the client and the server have a unique name called Principal. At the same time, the client and server have their own passwords, and their passwords are known only to themselves and the authentication server AS.

Basic concepts
----------------------------------------
- Principal (security individual)
    - The authenticated individual has a name and password
- KDC (Key Distribution Center)
    - Network service that provides tickets and temporary session keys
- Ticket
    - A record that a user can use to prove his or her identity to the server, including the user's identity, session key, timestamp, and other information. Most of the information in the Ticket is encrypted and the key is the server's key
- Authenticator
    - A record containing some recently generated information using a session key shared between the user and the server
- Credentials
    - A ticket plus a secret session key
- Authentication Server (AS)
    - Authenticate users via long-term key
    - AS gives the user ticket granting ticket and short-term key
    - Authentication services
- Ticket Granting Server (TGS)
    - Authenticate users via short-term key and Ticket Granting Ticket
    - TGS issues tickets to users to access other servers
    - Authorization and access control services

Simplified certification process
----------------------------------------
1. The client initiates a request to the server. The request content is: client’s principal, server’s principal
2. After AS receives the request, it randomly generates a password Kc, s (session key), and generates the following two tickets and returns them to the client.
    1. The ticket given to the client is encrypted with the client's password. The content is random password, session, server_principal.
    2. The ticket to the server is encrypted with the server's password, and the content is random password, session, client_principal
3. After the client obtains the two tickets in the second step, it first uses its own password to decrypt the tickets and obtains Kc, s, and then generates an Authenticator, which mainly includes the current time and the check code of Ts, c, and encrypts it with SessionKey Kc, s. Afterwards, the client sends the Authenticator and the ticket to the server to the server at the same time.
4. The server first uses its own password to unlock the ticket, gets the SessionKey Kc,s, then uses Kc,s to unlock the Authenticator, and does the following checks
    1. Check whether the timestamp in the Authenticator is within 5 minutes of the current time, and check whether the timestamp appears for the first time. If this timestamp does not appear for the first time, it means that someone has intercepted the content sent by the previous client and carried out a Replay attack.
    2. Check whether the checksum is correct
    3. If everything is correct, the client has passed the authentication.
5. The server segment can optionally reply a message to the client to complete two-way authentication. The content is a timestamp encrypted with the session key.
6. The client verifies the server by decrypting the message and comparing the timestamp sent back with the timestamp sent by itself.

Complete certification process
----------------------------------------
The process described above has been able to complete mutual authentication between the client and the server. However, what is more inconvenient is that each authentication requires the client to enter its own password.

Therefore, in the Kerberos system, a new role is introduced called: Ticket Granting Service (TGS - Ticket Granting Service). Its status is similar to an ordinary server, except that the service it provides is to issue tickets for clients to authenticate with other servers.

In this way, there are four roles in the Kerberos system: authentication server (AS), client (Client), common server (Server) and ticket authorization service (TGS). In this way, the authentication process for the client's initial communication with the server is divided into the following six steps:

1. The client initiates a request to the AS. The request content is: the principal of the client and the principal of the ticket authorization server.
2. After AS receives the request, it randomly generates a password Kc, s (session key), and generates the following two tickets and returns them to the client:
    1. The ticket given to the client is encrypted with the client's password, and the content is random password, session, tgs_principal
    2. The ticket to tgs is encrypted with tgs password, and the content is random password, session, client_principal
3. After the client obtains the two tickets in the second step, it first uses its own password to decrypt the tickets and obtains Kc, s, and then generates an Authenticator, which mainly includes the current time and the check code of Ts, c, and encrypts it with SessionKey Kc, s. Then the client initiates a request to tgs, the content includes:
    1. Authenticator
    2. The ticket for tgs is sent to the server at the same time
    3. server_principal
4. TGS first uses its own password to unlock the ticket, gets the SessionKey Kc,s, then uses Kc,s to unlock the Authenticator, and does the following checks
    1. Check whether the timestamp in the Authenticator is within 5 minutes of the current time, and check whether the timestamp appears for the first time. If this timestamp does not appear for the first time, it means that someone has intercepted the content sent by the previous client and carried out a Replay attack.
    2. Check whether the checksum is correct
    3. If everything is correct, the client has passed the authentication.
5. tgs generates a session key to assemble two tickets to the client
    1. The ticket encrypted with the session key of the client and tgs, including the newly generated session key and server_principal
    2. The ticket encrypted with the server's password, including the newly generated session key and client principal
6. After receiving the two tickets, the client unblocks its own, then generates an Authenticator and sends a request to the server. The content includes
    1. Authenticator
    2. Ticket to server
7. After the server receives the request, it uses its own password to decrypt the ticket, obtains the session key, and then uses the session key to decrypt the authenticator pair for unwarranted verification.
8. The server can choose to return a previous timestamp encrypted with the session key to complete two-way verification.
9. The client verifies the server by decrypting the message and comparing the timestamp sent back with the timestamp sent by itself.

Advantages and Disadvantages
----------------------------------------

advantage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Passwords are not easily eavesdropped
- Passwords are not transmitted online
- Password guessing is more difficult
- It is difficult to use the ticket after it is stolen because it needs to be used with the authentication header.

shortcoming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Lack of undo mechanism
-Introduced complex key management
- Requires clock synchronization
- Limited scalability

Reference link
----------------------------------------

specification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 1510 The Kerberos Network Authentication Service <https://tools.ietf.org/html/rfc1510>`_
- `Detailed explanation of Kerberos authentication process <https://blog.csdn.net/jewes/article/details/20792021>`_

attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Delegate to the Top: Abusing Kerberos for arbitrary impersonations and RCE <https://www.blackhat.com/docs/asia-17/materials/asia-17-Hart-Delegate-To-The-Top-Abusing-Kerberos-For-Arbitrary-Impersonations-And-RCE-wp.pdf>`_
- `Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol <https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94?redirectedfrom=MSDN>`_
- `Kerberos Technical Supplement for Windows <https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff649429(v=pandp.10)>`_
- `Cracking Kerberos TGS Tickets Using Kerberoast – Exploiting Kerberos to Compromise the Active Directory Domain <https://adsecurity.org/?p=2293>`_
