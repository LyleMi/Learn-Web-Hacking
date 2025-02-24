SSO
========================================

Introduction
----------------------------------------
Single Sign-On (SSO) refers to a user who can access multiple related but independent systems through a single ID and credentials (password).

Common Processes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. The user initiates a request to the service provider
2. SP redirects User to SSO identity verification service (Identity Provider)
3. User logs in via IP
4. The IP returns the credentials to User
5. User sends the credentials to SP
6. SP returns protected resources to users

The credential must have the following attributes

- The signature of the issuer
- Identity of the credentials
- Time of use
- Expiration time
- Effective time

Possible attacks/vulnerabilities
----------------------------------------

Information leakage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the SP and IP are previously transmitted using plaintext, it may be stolen.

Forged
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the key information is not signed during the communication process, it is easy to be forged.
