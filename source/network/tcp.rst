TCP protocol
========================================

Introduction
----------------------------------------
TCP (Transmission Control Protocol) is a connection-oriented, reliable, byte stream-based transport layer communication protocol, defined by RFC 793.

three handshakes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Three-Way Handshake means that when establishing a TCP connection, the client and server need to send a total of 3 packets to confirm the establishment of the connection.

In the first handshake, the client sets the flag SYN to 1, randomly generates a value seq=s, and sends the data packet to the server. The client enters the SYN_SENT state and waits for confirmation from the server.

After receiving the data packet in the second handshake, the server knows that the client requests to establish a connection from the flag bit SYN=1. The server sets both the flag bits SYN and ACK to 1, ack=s+1, randomly generates a value seq=k, and sends the data packet to the client to confirm the connection request. The server enters the SYN_RCVD state.

After receiving the confirmation for the third handshake, the client checks whether the ack value is s+1 and whether the ACK flag is 1. If it is correct, it sets the ACK flag to 1, ack=k+1, and sends the data packet to the server. The server checks whether the ack value is k+1 and whether the ACK flag is 1. If it is correct, the connection is successfully established. The client and server enter the ESTABLISHED state and complete the three-way handshake.

wave four times
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Four-Way Wavehand means that when a TCP connection is disconnected, the client and server need to send a total of 4 packets to confirm the disconnection.

When waving for the first time, the client sends a FIN to close the data transfer from the client to the server, and the client enters the FIN_WAIT_1 state.

After receiving the FIN for the second wave, the server sends an ACK to the client. The confirmation sequence number is the received sequence number + 1, and the server enters the CLOSE_WAIT state.

For the third time, the server sends a FIN to close the data transmission from the server to the client, and the server enters the LAST_ACK state.

After the client receives the FIN for the fourth wave, the client enters the TIME_WAIT state, and then sends an ACK to the server. The confirmation sequence number is the received sequence number + 1. The server enters the CLOSED state and completes four waves.

congestion control
----------------------------------------
Congestion refers to the phenomenon that the number of packets in the network is too large and the server has no time to process them, causing performance degradation of this part and even the entire network. In severe cases, it may even cause the network communication service to come to a standstill or a deadlock.

TCP uses a congestion control algorithm to reduce or avoid the occurrence of congestion. TCP's congestion algorithm has been implemented in a variety of ways, including Tahoe, Reno, NewReno, Vegas, Hybla, BIC, CUBIC, SACK, Westwood, PRR, BBR, etc.

Reference link
----------------------------------------
- `RFC 793 TRANSMISSION CONTROL PROTOCOL <https://tools.ietf.org/html/rfc793>`_
- `RFC 2001 TCP Slow Start, Congestion Avoidance, Fast Retransmit, and Fast Recovery Algorithms <https://tools.ietf.org/html/rfc2001>`_
- `RFC 3390 Increasing TCP's Initial Window <https://tools.ietf.org/html/rfc3390>`_
- `RFC 5681 TCP Congestion Control <https://tools.ietf.org/html/rfc5681>`_
- `TCP congestion control wiki <https://en.wikipedia.org/wiki/TCP_congestion_control>`_
