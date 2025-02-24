ADCS
========================================

introduce
----------------------------------------
Active Directory Certificate Services (AD CS) is a service that Microsoft uses to implement PKI.

Certificate
----------------------------------------
The certificate in ADCS is a digitally signed document in X.509 format for encryption, signature, or authentication, etc.

Commonly used attributes of certificates are composed of the following fields

- Subject: Subject
- Public Key: Public Key
- Extended Key Usages (EKUs): Extended key, object identifier that describes the certificate (Object identifier, OID)
- ...

Commonly used EKU OIDs include:

- Code Signing
- OID 1.3.6.1.5.5.7.3.3
- Certificates are used to sign executable code
- Encrypted file system
- OID 1.3.6.1.4.1.311.10.3.4
- Certificates are used to encrypt file systems
- Secure Email
- OID 1.3.6.1.5.5.7.3.4
- Certificates are used to encrypt emails
- Client authentication
- OID 1.3.6.1.5.5.7.3.2
- Smart card login
- OID 1.3.6.1.4.1.311.20.2.2
- Server Authentication
- OID 1.3.6.1.5.5.7.3.1
- Certificates are used to identify servers (such as HTTPS certificates)

Certificate Template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Microsoft provides the function of a certificate template to facilitate issuing certificates within the domain. A certificate template is a collection of registration policies and predefined certificate settings, including information such as certificate validity period, purpose, applicant, etc.

Certificate registration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Certificates can be registered in the following ways:

- Through Windows Client Certificate Registration Protocol (MS-WCCE)
- Remote Protocol (MS-ICPR) via ICertPassage
- Register with the Web service when ADCS has enabled the corresponding Web service
- Register through Certificate Registration Service (CES) when the corresponding service is installed on the server
- When the server has installed the corresponding service, use the network device to register the service
