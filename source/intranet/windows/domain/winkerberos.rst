Windows implementation of Kerberos
========================================

Related definitions
----------------------------------------

SPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Service Principal Names (SPN) are unique identifiers of service instances (such as HTTP, SMB, etc.).

SPN is divided into two types: one is registered under the machine account of Active Directory. When the permission of a service is Local System or Network Service, the SPN is registered under the machine account. One is to register under the domain user account of Active Directory. When the authority of a service is a domain user, the SPN is registered under the domain user account.
