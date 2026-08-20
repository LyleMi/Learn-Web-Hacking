Related vulnerabilities
----------------------------------------

DNS hijacking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are many ways to hijack DNS. The early attack methods are to attack domain name resolution servers or forge DNS responses to resolve domain names to malicious IP addresses.

With the continuous development of Internet applications, hijacking methods based on abandoned records have emerged. The scenario where this happens is that the resolution record of the secondary domain name points to a third-party resource, and after the third-party resource is released, the resolution record is not cancelled. In this scenario, you can apply for a third-party resource to gain the ability to control the resolution record.

Denial of service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS services usually open UDP ports. When the DNS server has a large number of secondary domain NS records, UDP reflection attacks through DNS can achieve high denial of service.
