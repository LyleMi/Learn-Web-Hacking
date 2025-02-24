domain
========================================
Domain refers to a logical environment that logically organizes multiple computers in the network and performs centralized management. A domain is the core management unit of organization and storage resources. In the domain, there is at least one domain controller, and the domain controller stores the user account and secure database of the entire domain.

Domain Structure
----------------------------------------

Domain Tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A domain tree is composed of multiple domains that share the same table structure and configuration, forming a continuous namespace.

Forest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Forests is a complex AD instance consisting of one or several domains, each domain tree has its own unique namespace.

Domain Controller
----------------------------------------
The ADDS directory is stored in the Domain Controller. There can be multiple domain controllers in a domain. Each domain controller has almost equal status and has almost the same database.

After adding a user account to a domain controller, the account will be automatically copied to the database of other domain controllers.

AD databases have multi-master Replication Model and single-host replication Model.

Multi-host mode can directly update AD objects in any domain controller and copy the updated objects to other domain controllers. Most of the data is copied in multi-host mode.

Single-host replication mode refers to a domain controller called an Operations Master responsible for receiving requests to change data and copying the data to other domain controllers.

trust
----------------------------------------
A trust relationship needs to be created between two domains in order to access resources in the corresponding domain.

Domain trust type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The trust methods of Active Directory can be divided into the following types:

- Tree-Root Trust
- Transferable in both directions
- Parent-Child Trust
- Transferable, two-way pedestrian
- Forest Trust
- If two forests create a trust relationship, all domains in the forest trust each other
- The trust relationship between two forests cannot be automatically extended to other forests
- Realm Trust
- ADDS domain can create trust between Kerberos domains on non-Windows systems
- External Trust
- The trust relationship can be created between domains located within two forests through external trust
- Shortcut Trust
- Can shorten the time to verify the user's identity

OR
----------------------------------------
Organization Unit (OU) is a container object that organizes objects in the domain into logical groups to help administrators manage. OU includes users, computers, work groups, printers, security policies, and other organizational units.
