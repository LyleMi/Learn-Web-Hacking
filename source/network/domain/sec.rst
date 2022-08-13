加密方案
----------------------------------------
作为主流的防御方案，DNS加密有五种方案，分别是 DNS-over-TLS (DoT)、DNS-over-DTLS、DNS-over-HTTPS (DoH)、DNS-over-QUIC以及DNSCrypt。

DoT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DoT方案在2016年发表于RFC7858，使用853端口。主要思想是Client和Server通过TCP协议建立TLS会话后再进行DNS传输，Client通过SSL证书验证服务器身份。

DNS-over-DTLS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-DTLS和DoT类似，区别在于使用UDP协议而不是TCP协议。

DoH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DoH方案在发表RFC8484，使用 ``https://dns.example.com/dns-query{?dns}``  来查询服务器的IP，复用https的443端口，流量特征比较小。DoH会对DNS服务器进行加密认证，不提供fallback选项。目前Cloudflare、Google等服务商对DoH提供了支持。

DNS-over-QUIC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS-over-QUIC安全特性和DoT类似，但是性能更高，目前没有合适的软件实现。

DNSCrypt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNSCrypt使用X25519-XSalsa20Poly1305而非标准的TLS，且DNSCrypt的Client需要额外的软件，Server需要的专门的证书。
