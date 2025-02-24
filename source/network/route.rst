Routing algorithm
========================================

Introduction
----------------------------------------
A routing algorithm is an algorithm used to find an optimal path from the source router to the destination router. There are multiple routing algorithms, and each algorithm has different impacts on network and router resources; since the routing algorithm uses multiple metrics, the optimal path selection for different routing algorithms is also different.

Functions of routing algorithm
----------------------------------------
Path selection between source/sink pairs and sending packets to their destination after the route is selected.

Requirements for routing algorithms:

- Correctness: Ensure packets are transferred from the source node to the destination node
- Simplicity: easy to implement, small hardware and software overhead
- Adaptive: also known as robustness, the algorithm can adapt to changes in traffic volume and network topology
- Stability: Can run for a long time without fault
- Fairness: Every node has the opportunity to transmit information
- Optimality: Try to choose a good route

Autonomous System AS (Autonomous System)
----------------------------------------
Classic definition:

- A complete set of routers and networks managed by an organization.
- Use a routing protocol within the AS and common metrics to determine the routes of packets within the AS.
- Use a routing protocol between AS to determine the routing of packets between ASs.

Although one AS uses multiple internal routing protocols and metrics, it exhibits a single and consistent routing policy for other AS.

Two major types of routing protocols
----------------------------------------
In the Internet, routing protocols can be divided into internal gateway protocol IGP (Interior Gateway Protocol) and external gateway protocol EGP (External Gateway Protocol).

IGP is a routing protocol used within an AS, such as RIP and OSPF protocols, which is an intradomain routing. When the source host and the destination host are in different AS, when the data report reaches the boundary of the AS, the external gateway protocol EGP is used to pass the routing information to another autonomous system, such as BGP-4, which is inter-domain routing ( intradomain routing).

RIP
----------------------------------------
Routing Information Protocol (RIP) is a routing protocol based on distance vectors. The RIP protocol requires that every router in the network maintain the distance from itself to every other destination network within the autonomous system and the next hop router address.

OSPF
----------------------------------------
Open Shortest Path First (OSPF), the algorithm is called "Shortest Path First" because it uses the shortest path algorithm SPF proposed by Dijkstra, which is just the name of a protocol, and it does not mean that other routing protocols are not "Shortest path first".
