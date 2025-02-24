Related vulnerabilities
----------------------------------------

DNS Hijacking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are many ways to hijack DNS. The earlier attack method was to resolve the domain name to a malicious IP address by attacking the domain name resolution server or forging DNS responses.

With the continuous development of Internet applications, hijacking methods based on abandoned records have emerged. The scenario in which this method occurs is that the secondary domain name resolution record points to the third-party resource. After the third-party resource is released, the resolution record is not cancelled. In this scenario, the corresponding application for third-party resources can be obtained to obtain the control analysis record ability.

Denial of service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS services usually open UDP ports. When the DNS server has a large number of secondary domain NS records, UDP reflection attacks through DNS can achieve high-power denial of service.
