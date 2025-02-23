JWT
========================================

Introduction
----------------------------------------
Json web token (JWT), a JSON-based open standard ((RFC 7519) implemented to pass declarations between network application environments. The token is designed to be compact and secure, especially suitable for single-purpose distributed sites. Sign-in (SSO) scenario. JWT statements are generally used to pass authenticated user identity information between identity providers and service providers to facilitate the acquisition of resources from the resource server, and may also add some additional business logic. The token can also be used for authentication or encrypted.

constitute
----------------------------------------
It is divided into three parts: header/payload/signature. where header is the declared type and the algorithm used for encryption. payload is the load, and finally add ``HMAC(base64(header)+base64(payload), secret)``

Security Question
----------------------------------------

Header section
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether to support modifying the algorithm to none/symmetric encryption algorithm
- Delete the signature
- Insert error message
- Add a new public key directly to the header
- Is there SQL injection/command injection/directory traversal in the kid field?
- Directly download the corresponding public and private key through kid in combination with business functions
- Is it possible to force the encryption algorithm on the whitelist
- JWKS Hijacking
- JKU (JWK Set URL) / X5U (X.509 URL) Injection

Payload section
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Whether sensitive information exists
- Check expired strategies such as ``exp``, ``iat``

Signature Part
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Check whether to check the signature for mandatory
- Can the key be blasted
- Can I get the key in other ways

other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Replay
- Time attack by matching time verification
- Modify the algorithm RS256 to HS256
- Weak key cracking

Reference link
----------------------------------------
- `Critical vulnerabilities in JSON Web Token libraries <https://auth0.com/blog/>`_
