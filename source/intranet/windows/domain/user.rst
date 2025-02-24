user
========================================

User Groups and Work Groups
----------------------------------------

user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are some users set up for specific purposes in Windows system, namely: SYSTEM, Trustedinstaller, Everyone, Creator Owner, etc. These special users do not belong to any user group. It is a completely independent account. Among them, SYSTEM has the account that manages the entire computer, and general operations cannot obtain the permissions equivalent to it.

User Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Windows systems have built-in many local user groups for managing user permissions. As long as the user account is added to the corresponding user group, the user account will also have the permissions owned by the corresponding user group.

By default, the system divides 7 groups for the user and gives different operation permissions to each group. These groups are: Administrators, High-Person Users, Normal Users, Backup Operators, File Replication Groups, Guests, Identity Authenticated Users.

Working Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Workgroups are the most commonly used simplest and most common resource management model. By default, computers are in workgroups called workgroups. The working group model is relatively loose, suitable for situations where the number of computers in the network is small and does not require strict management.

Users in the domain
----------------------------------------

Domain User
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users in a domain environment have different accounts from local users, and domain user accounts are saved in the active directory. In a domain environment, a domain user can log in on any computer in the domain. In the domain, users can use SID (Security Identifier) to indicate their identity, and use NTLM hash or Kerberos to verify their identity.

Machine User
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Machine users are also called machine accounts or computer accounts. All hosts joining the domain will have a machine user, and the user name of the machine user ends with ``$``.

Group Policy
----------------------------------------
Group Policy is used to control the working environment of user accounts and computer accounts. Group Policy provides centralized management and configuration of user settings in operating systems, applications, and active directories. The local group policy (LGPO or LocalGPO) can manage group policy objects on independent and non-domain computers. Group policies in domain environments are often called GPOs (Group Policy Object).
