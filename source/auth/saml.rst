SAML
========================================

Introduction
----------------------------------------
SAML (Security Assertion Markup Language) is a language in xXML format that uses XML format interaction to complete the functions of SSO.

There are two versions 1.1 and 2.0 in SAML, which are incompatible, but are roughly the same in terms of logical concepts or object structures, but there are differences in some details.

Certification process
----------------------------------------
SAML authentication involves three roles, namely service provider (SP), authentication service (IDP), and user (Client). A typical authentication process is as follows:

1. Client accesses protected resources
2. SP generates authentication request SAML to return to Client
3. Client submits a request to IDP
4. IDP returns authentication request
5. Client login IDP
6. After the authentication is successful, IDP generates a private key signature that identifies the permissions SAML and returns it to the Client.
7. Client submits SAML to SP
8. SP reads SAML, confirms that the request is legal, and returns the resource

Security Question
----------------------------------------
- From the authentication option in SSL mode, you can delete the signature tag to bypass authentication
- If expiration is missing in SAML and the assertion that the ID is not unique, it may be affected by a replay attack

Reference link
----------------------------------------
- `Saml Wiki <https://en.wikipedia.org/wiki/saml_2.0>` _
- Apply, "you will be shrouded: //
- `SSO Wars The Token Menace <https://i.blackhat.com/USA-19/Wednesday/us-19-Munoz-SSO-Wars-The-Token-Menace.pdf>`_
