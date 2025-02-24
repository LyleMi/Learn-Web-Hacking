the term
----------------------------------------

mDNS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Multicast DNS (mDNS), multicast DNS, uses port 5353, multicast address is ``224.0.0.251`` or ``[FF02::FB]``. mDNS can be used in a small network without a regular DNS server to implement DNS-like programming interfaces, package formats, and operational semantics. The packet structure of mDNS protocol is the same as that of DNS, but some fields have new meanings for mDNS.

The host that starts mDNS multicasts messages to all hosts after entering the LAN, including host name, IP and other information. Other hosts with corresponding services will also respond to information containing host name and IP.

The domain name of mDNS is distinguished from the normal domain name by ``.local``.

FQDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FQDN (Fully-Qualified Domain Name) is the complete form of a domain name, mainly containing zero-length root tags, such as ``www.example.com.``.

TLD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Top-Level Domain (TLD) is a domain belonging to the root domain, such as ``com`` or ``jp``.

TLDs can generally be divided into Country Code Top-Level Domains (ccTLDs), Generic Top-Level Domains (gTLDs), and others.

IDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Internationalized Domain Names for Applications (IDNA) is to handle non-ASCII characters.

CNAME
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CNAME is Canonical name, also known as alias, which points the domain name to another domain name.

TTL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Time To Live, unsigned integer, record the time when DNS records expire, the minimum is 0, and the maximum is 2147483647 (2^31 - 1).
