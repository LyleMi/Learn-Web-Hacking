Network Basics
========================================

The composition of computer communication network
----------------------------------------
The computer network consists of a communication subnet and a resource subnet. Among them, the communication subnet is responsible for error-free and orderly transmission of data, and its processing functions include error control, traffic control, routing, network interconnection, etc.

Among them, the resource subnet is the local system environment for computer communication, including hosts, terminals and applications, etc. The main functions of the resource subnet are user resource configuration, data processing and management, software and hardware sharing, and load balancing.

In general, a computer communication network is a system that transmits and shares various information of the resource subnet by a communication subnet.

Communication Protocol
----------------------------------------
In order to complete the orderly information exchange between computers, the concept of communication protocol was proposed, which is defined as a complete set of rules that both parties (or parties) who communicate with each other must abide by on how to conduct an information exchange.

The agreement involves three elements, namely:

- Syntax: Syntax is the structure and format of user data and control information, as well as the meaning of the order in which data appears
- Semantics: Used to explain the meaning of each part of the bitstream
- Timing: Detailed description of event implementation order

OSI seven-layer model
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
OSI (Open System Interconnection) is divided into seven layers: physical layer, data link layer, network layer, transmission layer, session layer, presentation layer, and application layer. Its specific functions are as follows.

Physical layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provides mechanical, electrical functions and procedures that are required to establish, maintain and release physical links
- Physical transmission, fault monitoring and physical layer management of data streams (bit streams) through transmission media
- Receive frames from the data link layer and convert bitstreams into signals on the underlying physical medium

Data link layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Transfer data between both ends of a physical link
- Provide data transmission functions and controls between network layer entities
- Provide data flow control
- Detect and correct errors caused by physical links
- Formatted messages are called frames

Network layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Responsible for end-to-end data routing or exchange, establishing connections for transparent transmission of data
- Address and resolve all issues related to data transmission between heterogeneous networks
- Functions using the above transport layer and the below data link layer
- Formatted messages are called grouping

Transport layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provide error-free data transmission
- Receive data from the session layer, split the data into smaller packets, transmit packets to the network layer and ensure that packets are complete and correctly reach their destinations
- Provide reliable and transparent data transmission between systems, providing end-to-end error recovery and traffic control

Session layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provides coordination of communication processes between nodes
- Responsible for executing session rules (such as whether the connection allows half-duplex or full-duplex communication), synchronizing data flow, and re-establishing the connection when a failure occurs
- Functions using the above presentation layer and the below transport layer

Expression layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provide data format, transformation and encoding conversion
- Syntax and semantics involving data being transferred
- Encode messages in a format suitable for electronic transmission
- Perform data compression and encryption of this layer
- Receive messages from the application layer, convert formats, and transmit them to the session layer, which is often merged in the application layer

Application layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Including various protocols that define specific user-oriented applications: such as email, file transfer, etc.

Summarize
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The lower three-layer model belongs to the communication subnet and involves providing transparent connections between users. The operation is mainly based on each link (hop-by-hop) to communicate on each data link between nodes. The network layer controls the communication on each link, but depends on the coordinated operations of other nodes.

The third layer of high school belongs to the resource subnet, which mainly involves ensuring that information is transmitted in a correct and comprehensible form.

The transport layer is the interface between the high-level and the low-level. It is the first end-to-end layer, ensuring transparent end-to-end connections, meeting the user's quality of service (QoS) requirements, and providing appropriate information to the high-level layer form.
