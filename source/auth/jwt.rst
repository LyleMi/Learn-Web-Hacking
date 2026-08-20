JWT
========================================

Introduction
----------------------------------------
Json web token (JWT) is a JSON-based open standard (RFC 7519). This token is designed to be compact and secure, especially suitable for single sign-on (SSO) scenarios on distributed sites. JWT claims are generally used to transfer authenticated user identity information between identity providers and service providers to facilitate obtaining resources from the resource server. Some additional claim information necessary for other business logic can also be added. The token can also be used directly for authentication and can also be encrypted.

constitute
----------------------------------------
It is divided into three parts, namely header/payload/signature. The header is the declared type and the algorithm used for encryption. payload is the load, and finally ``HMAC(base64(header)+base64(payload), secret)`` is added

Security Question
----------------------------------------

Header part
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether to support changing the algorithm to none/symmetric encryption algorithm
- Delete signature
- Insert error message
- Add the new public key directly to the header
- Whether there is SQL injection/command injection/directory traversal in the kid field
- Combined with business functions, directly download the corresponding public and private keys through kid
- Whether to force the use of encryption algorithms on the whitelist
- JWKS hijack
- JKU (JWK Set URL) / X5U (X.509 URL) injection

Payload part
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether there is sensitive information in it
- Check expiration policies, such as ``exp``, ``iat``

Signature part
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Check if signature checking is mandatory
- Whether the key can be exploded
- Is there any other way to get the key?

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Replay
- Time attack by matching the verified time
- Modify the algorithm RS256 to HS256
- Weak key cracking

Reference link
----------------------------------------
- `Critical vulnerabilities in JSON Web Token libraries <https://auth0.com/blog/>`_
