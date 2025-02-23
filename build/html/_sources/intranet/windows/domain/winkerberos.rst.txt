Kerberos' Windows implementation
========================================

Related definitions
----------------------------------------

SPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ServicePrincipal Names (SPN) is a unique identifier for service instances (such as HTTP, SMB, etc.).

SPNs are divided into two types: one is to register under the machine account in the active directory. When a service's permissions are Local System or Network Service, SPN is registered under the machine account. One is to register under the domain user account in the active directory. When a service's permissions are a domain user, the SPN is registered under the domain user account.
