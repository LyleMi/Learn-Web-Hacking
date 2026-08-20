Network basics
========================================

Composition of computer communication network
----------------------------------------
A computer network consists of a communication subnet and a resource subnet. The communication subnet is responsible for error-free and orderly transmission of data, and its processing functions include error control, flow control, routing, network interconnection, etc.

The resource subnet is the local system environment for computer communication, including hosts, terminals, and applications. The main functions of the resource subnet are user resource configuration, data processing and management, software and hardware sharing, and load balancing.

In general, a computer communication network is a system that is carried by a communication subnet and transmits and shares various types of information in resource subnets.

Communication protocol
----------------------------------------
In order to complete the orderly exchange of information between computers, the concept of communication protocol is proposed, which is defined as a set of rules that two parties (or multiple parties) communicating with each other must abide by on how to exchange information.

The agreement involves three elements, namely:

- Grammar: Grammar is the structure and format of user data and control information, as well as the meaning of the order in which the data appears.
- Semantics: used to explain the meaning of each part of the bitstream
- Timing: Detailed description of the sequence of event implementation

OSI seven-layer model
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
OSI (Open System Interconnection) is divided into seven layers: physical layer, data link layer, network layer, transport layer, session layer, presentation layer and application layer. Its specific functions are as follows.

physical layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provides the mechanical, electrical functions and procedures required to establish, maintain and release physical links.
- Physical transmission, fault monitoring and physical layer management of data streams (bit streams) through transmission media
- Receive frames from the data link layer and convert the bit stream into signals on the underlying physical medium

data link layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-Transfer data between two ends of a physical link
- Provide data transmission functions and control between network layer entities
- Provide data flow control
- Detect and correct errors caused by physical links
-Formatted messages are called frames

network layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Responsible for end-to-end data routing or switching, establishing connections for transparent transmission of data
- Address and resolve all issues related to data transfer across heterogeneous networks
- Use the functionality of the transport layer above and the data link layer below
-Formatted messages are called packets

transport layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provides error-free data transfer
- Receive data from the session layer, split the data into smaller packets if necessary, deliver the packets to the network layer and ensure that the packets arrive complete and correctly at their destination
- Provide reliable and transparent data transmission between systems, providing end-to-end error recovery and flow control

session layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provide coordination of the communication process between nodes
- Responsible for enforcing session rules (such as whether the connection allows half-duplex or full-duplex communication), synchronizing data flows, and re-establishing connections when failures occur
- Use the functionality of the presentation layer above and the transport layer below

presentation layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Provide data formats, transformations and encoding conversions
- Involves the syntax and semantics of the data being transferred
- Encode the message in a format suitable for electronic transmission
- Perform data compression and encryption for this layer
- Receive messages from the application layer, convert the format, and transmit them to the session layer, which is often merged with the application layer

Application layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Includes various protocols that define specific user-facing applications: e-mail, file transfer, etc.

Summarize
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The lower three-layer model belongs to the communication subnet and involves providing transparent connections between users. The operation is mainly based on each link (hop-by-hop) and communicates on each data link between nodes. The network layer controls communication on each link, but relies on the coordinated operations of other nodes.

The upper three layers belong to the resource subnet and are mainly concerned with ensuring that information is transmitted in a correct and understandable form.

The transport layer is the interface between the upper three layers and the lower three layers. It is the first end-to-end layer, ensuring transparent end-to-end connections, meeting the user's quality of service (QoS) requirements, and providing appropriate information forms to the upper three layers.
