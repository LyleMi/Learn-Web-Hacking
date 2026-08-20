domain
========================================
A domain refers to a logical environment that logically organizes multiple computers in the network together for centralized management. A domain is the core management unit for organizing and storing resources. In a domain, there is at least one domain controller. The domain controller stores user accounts and security databases for the entire domain.

domain structure
----------------------------------------

domain tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Domain trees (Trees) are composed of multiple domains that share the same table structure and configuration to form a continuous namespace.

Forest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Forests are a complex AD instance, consisting of one or several domains. Each domain tree has its own unique namespace.

domain controller
----------------------------------------
The ADDS directory is stored in the Domain Controller. There can be multiple domain controllers in a domain. Each domain controller has almost equal status and has almost the same database.

After a user account is added to one domain controller, the account is automatically copied to the databases of other domain controllers.

AD database has multi-master replication model (Multi-master Replication Model) and single-master replication model (Sing-master Replication Model).

Multi-master mode can directly update AD objects in any domain controller and copy the updated objects to other domain controllers. Most data is copied using multi-master mode.

The single-master replication mode means that a domain controller called the Operations Master is responsible for receiving requests to change data and replicating the data to other domain controllers.

trust
----------------------------------------
A trust relationship needs to be established between two domains before resources in the corresponding domain can be accessed.

Domain trust type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Active Directory trust methods can be divided into the following types:

- Tree-Root Trust
    - Transferable in both directions
- Parent-Child Trust
    - Transferable, two-way pedestrian
- Forest Trust
    - If two forests create a trust relationship, all domains in the forest trust each other
    - Trust relationships between two forests cannot be automatically extended to other forests
- Realm Trust
    - ADDS domains can create trusts with Kerberos domains on non-Windows systems
- External Trust
    - Trust relationships can be created between domains located in two forests through external trusts
- Shortcut Trust
    - Can shorten the time to verify user identity

OU
----------------------------------------
Organization Unit (OU) is a container object that organizes objects in the domain into logical groups to help administrators manage them. OU contains users, computers, workgroups, printers, security policies, and other organizational units.
