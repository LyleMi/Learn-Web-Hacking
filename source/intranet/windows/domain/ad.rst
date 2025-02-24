Active Directory
========================================
Active Directory (AD) is a directory service for Windows Server. Active Directory stores information about network objects and enables administrators and users to find and use this information.

ADDS
----------------------------------------
The component that Active Directory provides directory services is called Active Directory Domain Services (ADDS), which is responsible for the storage, addition, deletion, modification and search of directory databases, and can be used in a variety of local area network and wide area network scenarios.

Logically, ADDS components can be divided into Partition, Schema, Domain, Domain tree, Forest, OU, and Container.

Partition, also known as naming context, is part of the AD DS database. Schema is the definition of data stored in ADDS. Container is an object that provides an organizational framework for ADDS.

From the implementation distinction, ADDS can be divided into Domain controller, Data store, Global catalog server, RODC (Read-only domain controller), Site, and Subnet.

Each domain controller has complete ADDS data, and each domain controller can process the modification of the data and synchronize it to other domain controllers.

The domain control will have a copy of the data (Data store) and is stored by default in the ``C:\Windows\NTDS`` directory.

Global catalog server is a domain control that stores global catalog. Catlog stores all objects of a multiple-domain forest in a read-only manner, which is used to accelerate search.

Namespace
----------------------------------------
A namespace is a defined area where information related to it can be found by name.

Objects and properties
----------------------------------------
Resources in ADDS exist in the form of objects (Objects), and objects describe their characteristics through attributes (Attrbute).
