routing algorithm
========================================

Introduction
----------------------------------------
A routing algorithm is an algorithm used to find the best path from a source router to a destination router. There are multiple routing algorithms, each of which has a different impact on network and router resources; because routing algorithms use multiple metrics, the best path selections for different routing algorithms are also different.

Routing Algorithm Functions
----------------------------------------
Path selection between source/destination pairs, and routing of messages to their destinations.

Routing algorithm requirements:

- Correctness: Ensure that the packet is transmitted from the source node to the destination node
- Simplicity: easy to implement, low software and hardware overhead
- Adaptability: also called robustness, the algorithm can adapt to changes in business volume and network topology
- Stability: able to operate without failure for a long time
- Fairness: every node has a chance to transmit information
- Optimality: try to choose good routes

Autonomous System AS (Autonomous System)
----------------------------------------
Classic definition:

- A complete set of routers and networks managed by one organization.
- Use an intra-AS routing protocol and common metrics to determine the route of packets within the AS.
- Use an inter-AS routing protocol to determine the routing of packets between ASs.

Although an AS uses multiple internal routing protocols and metrics, it exhibits a single and consistent routing strategy to other ASs.

Two major categories of routing protocols
----------------------------------------
In the Internet, routing protocols can be divided into interior gateway protocol IGP (Interior Gateway Protocol) and exterior gateway protocol EGP (External Gateway Protocol).

IGP is a routing protocol used within an AS, such as RIP and OSPF protocols, and is intradomain routing. When the source host and destination host are in different ASs, when the datagram reaches the boundary of the AS, the external gateway protocol EGP is used to transfer the routing information to another autonomous system, such as BGP-4, which is intradomain routing.

RIP
----------------------------------------
Routing Information Protocol (RIP) is a distance vector-based routing protocol. The RIP protocol requires each router in the network to maintain the distance and next-hop router address from itself to every other destination network in the autonomous system.

OSPF
----------------------------------------
Open Shortest Path First (OSPF), this algorithm is called "Shortest Path First" because it uses the shortest path algorithm SPF proposed by Dijkstra. It is just the name of a protocol. It does not mean that other routing protocols are not "Shortest Path First".
