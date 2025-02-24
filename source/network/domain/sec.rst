Encryption scheme
----------------------------------------
As a mainstream defense solution, there are five solutions for DNS encryption, namely DNS-over-TLS (DoT), DNS-over-DTLS, DNS-over-HTTPS (DoH), DNS-over-QUIC and DNSCrypt.

DoT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DoT solution was published in RFC7858 in 2016 and uses port 853. The main idea is that the Client and Server establish a TLS session through the TCP protocol before performing DNS transmission, and the Client verifies the server identity through the SSL certificate.

DNS-over-DTLS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-DTLS is similar to DoT, with the difference being using the UDP protocol instead of the TCP protocol.

DoH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DoH solution is publishing RFC8484, using ``https://dns.example.com/dns-query{?dns}`` to query the server's IP, multiplex the 443 port of https, and has relatively small traffic characteristics. DoH will encrypt and authenticate the DNS server and does not provide the fallback option. Currently, Cloudflare, Google and other service providers have provided support for DoH.

DNS-over-QUIC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-QUIC security features are similar to DoT, but have higher performance and currently there is no suitable software implementation.

DNSCrypt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNSCrypt uses X25519-XSalsa20Poly1305 instead of standard TLS, and DNSCrypt's client requires additional software and a dedicated certificate required by the Server.
