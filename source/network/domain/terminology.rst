the term
----------------------------------------

mDNS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Multicast DNS (mDNS), multicast DNS, uses port 5353, and the multicast address is ``224.0.0.251`` or ``[FF02::FB]``. mDNS can be used in a small network without conventional DNS servers to implement DNS-like programming interfaces, packet formats, and operational semantics. The message structure of mDNS protocol is the same as that of DNS, but some fields have new meanings for mDNS.

The host that starts mDNS will multicast messages to all hosts after entering the LAN, including host name, IP and other information. Other hosts with corresponding services will also respond with information containing host name and IP.

mDNS domain names are distinguished from ordinary domain names by ``.local``.

FQDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
FQDN (Fully-Qualified Domain Name) is the complete form of a domain name, which mainly contains a zero-length root tag, such as ``www.example.com.``.

TLD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A Top-Level Domain (TLD) is a domain that belongs to the root domain, such as ``com`` or ``jp``.

TLDs can generally be divided into Country Code Top-Level Domains (ccTLDs), Generic Top-Level Domains (gTLDs) and others.

IDN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Internationalized Domain Names for Applications (IDNA) is designed to handle the case of non-ASCII characters.

CNAME
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CNAME is Canonical name, also known as alias, which points a domain name to another domain name.

TTL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Time To Live, an unsigned integer, records the expiration time of DNS records. The minimum is 0 and the maximum is 2147483647 (2^31 - 1).
