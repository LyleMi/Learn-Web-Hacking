Email protocol suite
========================================

Introduction
----------------------------------------

SMTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SMTP (Simple Mail Transfer Protocol) is an email transfer protocol and a set of specifications for transferring emails from a source address to a destination address. When SSL is not enabled, the port number is 25. When SSL is enabled, the port number is mostly 465 or 994.

POP3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
POP3 (Post Office Protocol 3) is used to support remote management of email on the server using a client. The port number is 110 when SSL is not enabled, and the port number is 995 when SSL is enabled.

IMAP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
IMAP (Internet Mail Access Protocol), the Interactive Mail Access Protocol, is one of the standard protocols for mail access similar to POP3. The difference is that after IMAP is turned on, the emails you receive on the email client will still be retained on the server. At the same time, operations on the client will be fed back to the server, such as deleting emails, marking them as read, etc., and the emails on the server will also take corresponding actions. The port number is 143 when SSL is not enabled, and the port number is 993 when SSL is enabled.

Protection strategy
----------------------------------------

SPF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sender Policy Framework (SPF) is an email authentication mechanism that is used to confirm whether an email is sent by a domain-authorized mail server to prevent someone from pretending to be a phishing or spam email. SPF allows administrators to set a DNS TXT record or SPF record to set the IP range of the outgoing email server. If any email is not sent from the authorized IP address specified above, it is likely that the email was not actually sent by the real sender.

DKIM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DomainKeys Identified Mail (DKIM) is a method of detecting forged email sender addresses. The sender will insert DKIM-Signature into the header of the email, and the recipient will verify the sender's information by querying the public key in the DNS record.

DMARC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Domain-based Message Authentication, Reporting and Conformance (DMARC) is an email authentication protocol that solves the problem of inconsistencies between the domain name displayed in the mail bar and the domain name verified. To pass the DMARC check, authentication with SPF or/and DKIM is required, and the domain name in the header address must match the authenticated domain name.

Reference link
----------------------------------------

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 4408 Sender Policy Framework (SPF) for Authorizing Use of Domains in E-Mail, Version 1 <https://tools.ietf.org/html/rfc4408>`_
- `RFC 6376 DomainKeys Identified Mail (DKIM) Signatures <https://tools.ietf.org/html/rfc6376>`_
- `RFC 7208 Sender Policy Framework (SPF) for Authorizing Use of Domains in Email, Version 1 <https://tools.ietf.org/html/rfc7208>`_
- `RFC 7489 Domain-based Message Authentication, Reporting, and Conformance (DMARC) <https://tools.ietf.org/html/rfc7489>`_
- `RFC 8301 Cryptographic Algorithm and Key Usage Update to DomainKeys Identified Mail (DKIM) <https://tools.ietf.org/html/rfc8301>`_
- `RFC 8463 A New Cryptographic Signature Method for DomainKeys Identified Mail (DKIM) <https://tools.ietf.org/html/rfc8463>`_
- `RFC 8616 Email Authentication for Internationalized Mail <https://tools.ietf.org/html/rfc8616>`_
- `RFC 8611 Mail <https://tools.ietf.org/html/rfc8611>`_

Related documents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Sender Policy Framework wikipedia <https://en.wikipedia.org/wiki/Sender_Policy_Framework>`_
- `DomainKeys Identified Mail wikipedia <https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail>`_
- `DMARC wikipedia <https://en.wikipedia.org/wiki/DMARC>`_

research article
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Composition Kills:A Case Study of Email Sender Authentication <http://i.blackhat.com/USA-20/Thursday/us-20-Chen-You-Have-No-Idea-Who-Sent-That-Email-18-Attacks-On-Email-Sender-Authentication-wp.pdf>`_
