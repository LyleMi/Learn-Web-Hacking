HTTPS
========================================

Introduction
----------------------------------------
HTTPS (HyperText Transfer Protocol over Secure Socket Layer) can be understood as HTTP+SSL/TLS, that is, the SSL layer is added under HTTP. The security basis of HTTPS is SSL.

Interaction
----------------------------------------

Certificate verification stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Browser initiates HTTPS request
- Server returns HTTPS certificate
- Where the certificate contains:
- Authority information
- Public Key
- Company Information
- Domain Name
- Valid period
- Fingerprint
- The client verifies whether the certificate is legal, and if it is not legal, it will prompt an alarm

Data transmission stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- When the certificate verification is valid, generate random numbers locally
- Encrypt random numbers through public key and transmit the encrypted random numbers to the server
- The server decrypts the random number through the private key
- The server constructs a symmetric encryption algorithm through random numbers sent by the client, encrypts and transmits the returned result content

CA
----------------------------------------
CA (Certificate Authority) is the agency that issues digital certificates. It is an authoritative institution responsible for issuing and managing digital certificates, and as a trusted third party in e-commerce transactions, it assumes the responsibility for verifying the legality of public keys in the public key system.
