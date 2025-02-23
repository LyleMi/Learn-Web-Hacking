Email security
========================================

Common concepts
----------------------------------------
Commonly used concepts for email security are SPF, DKIM and DMARC. Among them, SPF (Sender Policy Framework) is a special DNS record that is used to set the legal IP for sending emails.

DKIM (DomainKeys Identified Mail) Adds digital signatures to the title of an email message, giving the mail server the ability to ensure that the content of the email is not changed. DKIM also exists in DNS. Query by querying txt record of ``<selector>._domainkey.example.com`.

DMARC(Domain-based Message Authentication): Query by querying ``<selector>._domainkey.example.com`.
