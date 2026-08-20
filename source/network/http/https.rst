HTTPS
========================================

Introduction
----------------------------------------
HTTPS (HyperText Transfer Protocol over Secure Socket Layer) can be understood as HTTP+SSL/TLS, that is, an SSL layer is added to HTTP. The security foundation of HTTPS is SSL.

interaction
----------------------------------------

Certificate verification phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The browser initiates an HTTPS request
- Server returns HTTPS certificate
- The certificate contains:
-Issuing authority information
- public key
- Company information
- Domain name
- Validity period
- Fingerprint
- The client verifies whether the certificate is legal and prompts an alarm if it is illegal.

Data transfer stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- When the certificate is verified to be legitimate, a random number is generated locally
- Encrypt the random number through the public key and transmit the encrypted random number to the server
- The server decrypts the random number through the private key
- The server constructs a symmetric encryption algorithm through the random numbers passed in by the client, and encrypts the returned result content before transmitting it.

CA
----------------------------------------
CA (Certificate Authority) is an organization that issues digital certificates. It is an authoritative organization responsible for issuing and managing digital certificates. As a trusted third party in e-commerce transactions, it assumes the responsibility of verifying the legality of public keys in the public key system.
