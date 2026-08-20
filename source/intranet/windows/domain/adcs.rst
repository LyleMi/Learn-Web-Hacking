ADCS
========================================

introduce
----------------------------------------
Active Directory Certificate Services (AD CS) is a service used by Microsoft to implement PKI.

Certificate
----------------------------------------
Certificates in ADCS are digitally signed documents in X.509 format, used for encryption, signature, or authentication, etc.

Commonly used attributes of certificates consist of the following fields

- Subject: subject
- Public Key: public key
- Extended Key Usages (EKUs): Extended keys that describe the object identifier (OID) of the certificate
- ...

Commonly used EKU OIDs include:

- Code signing
    - OID 1.3.6.1.5.5.7.3.3
    - Certificate is used to sign executable code
- Encrypted file system
    - OID 1.3.6.1.4.1.311.10.3.4
    - Certificate is used to encrypt the file system
- Secure email
    - OID 1.3.6.1.5.5.7.3.4
    - Certificate used to encrypt emails
- Client authentication
    - OID 1.3.6.1.5.5.7.3.2
- Smart card login
    - OID 1.3.6.1.4.1.311.20.2.2
- Server authentication
    - OID 1.3.6.1.5.5.7.3.1
    - Certificate used to identify the server (e.g. HTTPS certificate)

certificate template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Microsoft provides the certificate template function to facilitate the issuance of certificates within the domain. A certificate template is a collection of registration policies and predefined certificate settings, including certificate validity period, purpose, applicant and other information.

Certificate registration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Certificates can be registered in the following ways:

- Via Windows Client Certificate Enrollment Protocol (MS-WCCE)
- Via ICertPassage remote protocol (MS-ICPR)
- When ADCS has enabled the corresponding web service, use the web service to register
- Register through the Certificate Enrollment Service (CES) when the corresponding service is installed on the server
- Use the network device registration service when the corresponding service is installed on the server
