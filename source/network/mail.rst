Mail Agreement Family
========================================

Introduction
----------------------------------------

SMTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SMTP (Simple Mail Transfer Protocol) is a protocol for email transmission, a set of specifications for transferring mail from source to destination address. The port number is 25 when SSL is not enabled, and the port number is mostly 465 or 994 when SSL is enabled.

Pop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
POP3 (Post Office Protocol 3) is used to support remote management of email on the server using the client. The port number is 110 when SSL is not enabled, and the port number is mostly 995 when SSL is enabled.

IMAP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
IMAP (Internet Mail Access Protocol), or the interactive mail access protocol, is one of the standard mail access protocols similar to POP3. The difference is that after IMAP is enabled, the emails you receive from the email client are still retained on the server, and the operations on the client will be fed back to the server, such as: deleting emails, marking them read, etc., on the server The email will also do the corresponding actions. The port number is 143 when SSL is not enabled, and the port number is mostly 993 when SSL is enabled.

Protection strategy
----------------------------------------

SPF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The Sender Policy Framework (SPF) is an email authentication mechanism used to confirm whether emails are sent by domain-authorized mail servers to prevent people from pretending to phish or sending spam. SPF allows administrators to set a DNS TXT record or SPF record to set the IP range of the sending mail server. If any email is not sent from the specified authorized IP address above, it is likely that the email is not actually sent by the real sender. Send it out.

DKIM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DomainKeys Identified Mail (DKIM) is a method to detect forgery of email sender addresses. The sender will insert DKIM-Signature into the header of the message, and the recipient will verify the sender's information by querying the public key in the DNS record.

DMARC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Domain-based Message Authentication, Reporting and Conformance (DMARC) is an email authentication protocol that resolves inconsistencies between domain names displayed in the mailing bar and the authenticated domain name. To pass the DMARC check, it must pass the authentication of SPF or/and DKIM, and the domain name in the header address must be consistent with the authenticated domain name.

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

Related Documents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Sender Policy Framework wikipedia <https://en.wikipedia.org/wiki/Sender_Policy_Framework>`_
- `DomainKeys Identified Mail wikipedia <https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail>`_
- `dmarc Wikipedia <https://en.wikipedia.org/wiki/dmarc>` _

Research Articles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Composition Kills:A Case Study of Email Sender Authentication <http://i.blackhat.com/USA-20/Thursday/us-20-Chen-You-Have-No-Idea-Who-Sent-That-Email-18-Attacks-On-Email-Sender-Authentication-wp.pdf>`_
