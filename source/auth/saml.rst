SAML
========================================

Introduction
----------------------------------------
SAML (Security Assertion Markup Language), translated as Security Assertion Markup Language, is an xXML format language that uses XML format interaction to complete the SSO function.

SAML exists in two versions, 1.1 and 2.0. These two versions are incompatible, but they are roughly equivalent in logical concepts or object structures, and only differ in some details.

Certification process
----------------------------------------
SAML authentication involves three roles, namely service provider (SP), authentication service (IDP), and user (Client). A typical certification process is as follows:

1. Client access protected resources
2. SP generates authentication request SAML and returns it to Client
3. Client submits request to IDP
4. IDP returns authentication request
5. Client logs in to IDP
6. After the authentication is successful, the IDP generates the SAML with the private key signature identifying the permissions and returns it to the Client.
7. Client submits SAML to SP
8. SP reads SAML, determines that the request is legal, and returns the resource

Security Question
----------------------------------------
- Due to the optionality of authentication in ssl mode, the signature method label can be deleted to bypass authentication
- If expiration is missing in SAML and the assertion ID is not unique, it may be affected by replay attacks

Reference link
----------------------------------------
- `SAML Wiki <https://en.wikipedia.org/wiki/SAML_2.0>`_
- `RFC7522 <https://tools.ietf.org/html/rfc7522>`_
- `SSO Wars The Token Menace <https://i.blackhat.com/USA-19/Wednesday/us-19-Munoz-SSO-Wars-The-Token-Menace.pdf>`_
