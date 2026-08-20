SSO
========================================

Introduction
----------------------------------------
Single sign-on (SingleSignOn, SSO) means that a user can access multiple related but independent systems through a single ID and credential (password).

Common processes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. The user initiates a request to the service provider (Service Provider)
2. SP redirects User to SSO identity verification service (Identity Provider)
3. User logs in via IP
4. IP returns the credentials to User
5. User sends the certificate to SP
6. SP returns the protected resources to the user

The certificate must have the following attributes

- Signature of the issuer
- Identity of the credential
- Time of use
    - Expiration time
    - Effective time

Possible attacks/vulnerabilities
----------------------------------------

information leakage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If SP and IP previously used clear text to transmit information, it may be stolen.

forgery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If key information is not signed during the communication process, it can be easily forged.
