Email security
========================================

Common concepts
----------------------------------------
Commonly used concepts in email security are SPF, DKIM and DMARC. Among them, SPF (Sender Policy Framework) is a special DNS record used to set the legal IP for sending emails.

DKIM (DomainKeys Identified Mail) adds a digital signature to the header of an email message, giving the mail server the ability to ensure that the content of the email has not changed. DKIM also exists in DNS. Query by querying the txt record of ``<selector>._domainkey.example.com``.

DMARC (Domain-based Message Authentication): Query by querying the txt record of ``<selector>._domainkey.example.com``.
