Domain name information
========================================

Whois
----------------------------------------
`Whois <https://www.whois.com/>`_ A database that can query whether a domain name is registered and the detailed information of the domain name is registered. Some useful information may exist, such as the domain name owner, the domain name registrar, Email, etc.

Search Engine Search
----------------------------------------
Search engines usually record domain name information, which can be queried through the syntax of ``site: domain``.

Third-party inquiry
----------------------------------------
There are quite a lot of third-party applications in the network that provide subdomain query functions. Here are some examples, and more websites can be found in the 8.1 tool list.

- `DNSDumpster <https://dnsdumpster.com/>`_
- `virusortal <https://www.virustom.com/>` _
- CrtSearch
- threatminer
- Censys

ASN information association
----------------------------------------
An Autonomous System (AS) in the network is a small unit that has the right to autonomously decide what routing protocol should be used in this system. This network unit can be a simple network or a network group controlled by one or more ordinary network administrators, which is a single managed network unit (such as a university, a business or a company) Individual).

An autonomous system is sometimes called a routing domain. An autonomous system will assign a globally unique 16-digit number, which is called the Autonomous System Number (ASN). Therefore, the possible related IP can be found through the ASN number, for example:

::

whois -h whois.radb.net -- '-i origin AS111111' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq
nmap --script targets-asn --script-args targets-asn.asn=15169

Domain name relevance
----------------------------------------
Multiple domain names registered by the same enterprise/individual are usually related, such as using the same email address to register, using the same filing, and the same person in charge to register, etc. This method can be used to find the associated domain names. . One operation step is as follows:

- Query the domain name registration email address
- Query the registration number through the domain name
- Query the domain name through the registration number
- Counter check the registration email
- Counter-check registrants
- The domain name query through the registrant is inquired about the email address
- Search the domain name through the previous email
- Query the subdomain of the domain name obtained above

In addition, when some companies register domain names, they will register domain names with different tlds, such as example.com / example.cn. However, the domain names of different tlds may also be registered by other people and need to be identified separately.


Website information utilization
----------------------------------------
There is quite a lot of information in the website, and some information may be exposed by the website itself, various security policies, settings, etc.

The interaction of the website itself is usually not limited to a single domain name, but will interact with other subdomains. For this case, other subdomain information in the site can be collected by crawling the website. This information usually appears in JavaScript files, resource file links, etc.

Website security policies such as cross-domain policies, CSP rules, etc. usually also contain information about relevant domain names. Sometimes multiple domain names use the same SSL/TLS certificate for convenience, so sometimes relevant domain name information can be obtained through the certificate.

HTTPS certificate
----------------------------------------

Certificate transparency
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To ensure that HTTPS certificates are not misissued or forged, the CA will record the certificates in a log that is publicly verified, tamperable and only attached content, and any interested party can view all certificates issued by the Authorization Center. Therefore, the relevant domain name can be obtained by querying the authorized certificate.

SAN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Subject Alternate Name (SAN), simply put, when multiple domain names are needed and used for various services, use SAN certificates more often. SAN allows the use of the subjectAltName field in a security certificate to associate multiple values with the certificate, which are called subject alternative names.

Domain Transmission Vulnerability
----------------------------------------
DNS domain transfer refers to the redundant backup server refreshing its own domain (zone) database using data from the primary server. This is to prevent the master server from affecting the resolution of the entire domain name when it is unexpectedly unavailable.

Generally speaking, domain transfer operations should only allow trusted backup DNS servers to initiate, but if authorization is misconfigured, any user can obtain domain name information for the entire DNS server. This error authorization is called a DNS domain transmission vulnerability.

Passive DNS
----------------------------------------
Passive DNS passively records responses from different domain name servers from recursive domain name servers to form a database. Using the Passive DNS database, you can know which IPs have been bound to the domain name, which domain names have been associated with, and when the domain name was the earliest/recently appeared, providing great help for testing. Virustotal, passivetotal, CIRCL and other websites all provide query of Passive DNS database.

General analysis
----------------------------------------
General parsing is to parse all A records of `*.example.com` to a certain IP address. This situation needs to be handled when enumerating subdomains in order to prevent a large number of invalid records from being generated.

Important records
----------------------------------------

CNAME
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CNAME is Canonical name, also known as alias, which points the domain name to another domain name. It may contain information about other related services. The CDN acceleration feature used by many websites takes advantage of this record.

MX Record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MX record is Mail Exchanger, which records the server address corresponding to the domain name when sending emails. Can be used to find SMTP server information.

NS Records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NS (Name Server) records are records of domain name servers, used to specify which DNS server the domain name is resolved.

SPF record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SPF (Sender Policy Framework) is a DNS record type proposed to prevent spam. It is a TXT type record that is used to register all IP addresses owned by a domain name for outgoing mail. Relevant IP information can be obtained through SPF records. The commonly used command is ``dig example.com txt``.

CDN
----------------------------------------

CDN verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You can determine whether the target uses CDN through ping in multiple places. Common websites include ``http://ping.chinaz.com/````https://asm.ca.com/en/ping.php` ` etc.

Domain name search
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The parent or child domain name of a domain name that uses a CDN does not necessarily use a CDN. You can find the corresponding IP in this way.

History search
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CDN may be launched after the website is online for a period of time. You can find the real IP by looking for domain name resolution records.

Email information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Email communication through social engineering methods and obtain the IP address from the email header. The IP address may be the real IP of the website or the target export IP.

Breast explosion
----------------------------------------
In environments such as intranet where the above skills are not easy to use, or when you want to monitor the launch of new domain names, you can find a valid domain name through batch attempts.

Cache detection technology
----------------------------------------
In enterprise networks, DNS servers are usually configured to provide domain name resolution services to hosts within the network. Domain name cache detection (DNS Cache Snooping) technology sends domain name resolution requests to these servers, but does not require the use of recursive mode to detect whether a domain name has been requested. This method can be used to detect whether certain software is used, especially security software.
