Active Directory
========================================
Active Directory (AD) is a directory service for Windows Server. Active Directory stores information about network objects and enables administrators and users to find and use this information.

ADDS
----------------------------------------
The component of Active Directory that provides directory services is called Active Directory Domain Services (ADDS), which is responsible for the storage, addition, deletion, modification, and query of directory databases. It can be used in a variety of local area network and wide area network scenarios.

Logically, the components of ADDS can be divided into Partition, Schema, Domain, Domain tree, Forest, OU, and Container.

Partition is also called naming context and is part of the AD DS database. Schema is the definition of data stored in ADDS. Container is the object that provides the organizational framework for ADDS.

From the perspective of implementation, ADDS can be divided into Domain controller, Data store, Global catalog server, RODC (Read-only domain controller), Site, and Subnet.

Each domain controller has complete ADDS data, and each domain controller can handle data modifications and synchronize them to other domain controllers.

The domain controller will have a copy of the data (Data store), which is stored in the ``C:\Windows\NTDS`` directory by default.

The global catalog server is a domain controller that stores the global catalog. The catlog stores all objects in a multiple-domain forest in a read-only manner to speed up searches.

namespace
----------------------------------------
A namespace is a defined area in which related information can be found by name.

Objects and Properties
----------------------------------------
Resources in ADDS all exist in the form of objects (Object), and objects describe their characteristics through attributes (Attrbute).
