encryption scheme
----------------------------------------
As a mainstream defense solution, there are five DNS encryption solutions, namely DNS-over-TLS (DoT), DNS-over-DTLS, DNS-over-HTTPS (DoH), DNS-over-QUIC and DNSCrypt.

DoT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DoT solution was published in RFC7858 in 2016, using port 853. The main idea is that the Client and Server establish a TLS session through the TCP protocol before performing DNS transmission, and the Client verifies the server's identity through the SSL certificate.

DNS-over-DTLS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-DTLS is similar to DoT, except that it uses UDP protocol instead of TCP protocol.

DoH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DoH solution is publishing RFC8484, using ``https://dns.example.com/dns-query{?dns}`` to query the server's IP, reusing the 443 port of https, and the traffic characteristics are relatively small. DoH will perform encryption authentication on the DNS server and does not provide a fallback option. Currently Cloudflare, Google and other service providers provide support for DoH.

DNS-over-QUIC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-QUIC security features are similar to DoT, but have higher performance. Currently, there is no suitable software implementation.

DNSCrypt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNSCrypt uses X25519-XSalsa20Poly1305 instead of standard TLS, and the DNSCrypt Client requires additional software and the Server requires a special certificate.
