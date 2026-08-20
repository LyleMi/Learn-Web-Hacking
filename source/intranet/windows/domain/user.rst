user
========================================

User groups and work groups
----------------------------------------

user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are some users set up for specific purposes in the Windows system, namely: SYSTEM (system), Trustedinstaller (trusted program module), Everyone (owner), Creator Owner (creator), etc. These special users do not belong to any user group and are completely independent accounts. Among them, SYSTEM has the account with management permissions for the entire computer, and ordinary operations cannot obtain equivalent permissions.

User group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows systems have many built-in local user groups for managing user permissions. As long as the user account is added to the corresponding user group, the user account will also have the permissions of the corresponding user group.

By default, the system divides users into 7 groups and gives each group different operating permissions. These groups are: Administrators, Power Users, Users, Backup Operators, Replicator, Guests, and Authenticated Users.

working group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Workgroup (Workgroup) is the most commonly used, simplest and most common resource management mode. By default, computers are in a workgroup named workgroup. The workgroup mode is relatively loose and suitable for situations where the number of computers in the network is small and strict management is not required.

Users in the domain
----------------------------------------

domain user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users in a domain environment have different accounts than local users. Domain user accounts are stored in Active Directory. In a domain environment, a domain user can log in on any computer in the domain. Users in the domain can use SID (Security Identifier) ​​to identify themselves, and use NTLM hash or Kerberos to verify their identity.

machine user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Machine users are also called machine accounts or computer accounts. All hosts that join the domain will have a machine user. The machine user's username ends with ``$``.

group policy
----------------------------------------
Group Policy is used to control the working environment of user accounts and computer accounts. Group Policy provides centralized management and configuration of user settings across operating systems, applications, and Active Directory. Among them, local Group Policy (LGPO or LocalGPO) can manage Group Policy objects on independent and non-domain computers. Group Policy in a domain environment is usually called GPO (Group Policy Object).
