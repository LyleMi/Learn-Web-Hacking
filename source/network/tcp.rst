TCP protocol
========================================

Introduction
----------------------------------------
TCP (Transmission Control Protocol) is a connection-oriented, reliable, byte stream-based transmission layer communication protocol defined by RFC 793.

Three handshakes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Three-Way Handshake means that when establishing a TCP connection, the client and server need to send a total of 3 packets to confirm the establishment of the connection.

The first handshake client sets the flag SYN to 1, randomly generates a value of seq=s, and sends the data packet to the server. The client enters the SYN_SENT state and waits for the server to confirm.

After the second handshake server receives the data packet, the flag bit SYN=1 knows that the client requests to establish a connection. The server sets the flag bit SYN and ACK to 1, ack=s+1, and randomly generates a value seq=k , and send the data packet to the client to confirm the connection request, and the server enters the SYN_RCVD state.

After the third handshake client receives the confirmation, check whether the ack value is s+1 and whether the ACK flag is 1. If it is correct, set the flag bit ACK to 1, ack=k+1, and send the packet. To the server, the server checks whether the ack value is k+1 and whether the ACK flag is 1. If it is correct, the connection is established successfully. The client and the server enter the ESTABLISHED state and complete three handshakes.

Four waves
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Four-Way Wavehand means that when disconnecting a TCP connection, the client and server need to send a total of 4 packets to confirm the disconnection of the connection.

The first time I waved my hand to send a FIN to close the data transmission from the client to the server, and the client entered the FIN_WAIT_1 state.

The second wave of the server sends an ACK to the client and confirms that the serial number is received +1, and the server enters the CLOSE_WAIT status.

The third wave of the server sends a FIN to close the data transmission from the server to the client, and the server enters the LAST_ACK state.

The fourth wave after the client receives the FIN, the client enters the TIME_WAIT state, and then sends an ACK to the server, confirming that the serial number is received, the server enters the CLOSED state, completing four waves.

Congestion Control
----------------------------------------
Congestion refers to the phenomenon that the number of messages in the network is too large, which makes the server unable to process it, causing the performance of this part and even the entire network to decline. In severe cases, it may even cause the network communication service to stop and then die-lock.

TCP uses congestion control algorithms to reduce or avoid the occurrence of congestion. TCP's congestion algorithm has been implemented in many ways, including Tahoe, Reno, NewReno, Vegas, Hybla, BIC, CUBIC, SACK, Westwood, PRR, BBR, etc.

Reference link
----------------------------------------
- `RFC 793 TRANSMISSION CONTROL PROTOCOL <https://tools.ietf.org/html/rfc793>`_
- `RFC 2001 TCP Slow Start, Congestion Avoidance, Fast Retransmit, and Fast Recovery Algorithms <https://tools.ietf.org/html/rfc2001>`_
- `RFC 3390 Increasing TCP's Initial Window <https://tools.ietf.org/html/rfc3390>`_
- `RFC 5681 TCP Congestion Control <https://tools.ietf.org/html/rfc5681>`_
- `TCP congestion control wiki <https://en.wikipedia.org/wiki/TCP_congestion_control>`_
