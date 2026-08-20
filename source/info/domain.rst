Domain name information
========================================

Whois
----------------------------------------
`Whois <https://www.whois.com/>`_ is a database that can query whether a domain name has been registered and the details of the registered domain name. There may be some useful information in it, such as the domain name owner, domain name registrar, email address, etc.

search engine search
----------------------------------------
Search engines usually record domain name information, which can be queried through the ``site: domain`` syntax.

Third party inquiry
----------------------------------------
There are quite a few third-party applications on the Internet that provide subdomain query functions. Here are some examples. More websites can be found in the 8.1 Tool List.

- `DNSDumpster <https://dnsdumpster.com/>`_
- `Virustotal <https://www.virustotal.com/>`_
- CrtSearch
- threatminer
- Censys

ASN information association
----------------------------------------
In a network, an Autonomous System (AS) is a small unit that has the authority to independently decide which routing protocol should be used in the system. This network unit can be a simple network or a network group controlled by one or more ordinary network administrators. It is an individually manageable network unit (such as a university, an enterprise or an individual company).

An autonomous system is sometimes called a routing domain. An autonomous system will be assigned a globally unique 16-digit number called an Autonomous System Number (ASN). Therefore, you can use the ASN number to find potentially relevant IPs, for example:

::

    whois -h whois.radb.net -- '-i origin AS111111' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq
    nmap --script targets-asn --script-args targets-asn.asn=15169

Domain name relevance
----------------------------------------
Multiple domain names registered by the same enterprise/individual usually have certain correlations. For example, the same email address is used to register, the same registration is used, the same person in charge is used to register, etc. You can use this method to find related domain names. One operation step is as follows:

- Check domain name registration email
- Query the registration number through domain name
- Query domain name by registration number
- Check registered email address
- Check the registrant
- The domain name queried through the registrant is in the query email
- Query the domain name through the email address in the previous step
- Query the subdomain name of the domain name obtained above

In addition, when registering domain names, some companies will register domain names with different TLDs, such as example.com / example.cn. However, domain names with different TLDs may also be registered by other people and need to be identified separately.


Utilization of website information
----------------------------------------
There is quite a lot of information in the website, and the website itself, various security policies, settings, etc. may expose some information.

The interaction of the website itself is usually not limited to a single domain name, but also interacts with other subdomains. In this case, you can crawl the website to collect information about other subdomains in the site. This information usually appears in JavaScript files, resource file links, etc.

Website security policies such as cross-domain policies, CSP rules, etc. usually also include information about related domain names. Sometimes multiple domain names use the same SSL/TLS certificate for convenience, so sometimes the relevant domain name information can be obtained through the certificate.

HTTPS certificate
----------------------------------------

certificate transparency
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to ensure that the HTTPS certificate will not be mistakenly issued or forged, the CA will record the certificate in a log that is publicly verifiable, cannot be tampered with, and can only append content. Any interested party can view all certificates issued by the authorized center. Therefore, the relevant domain name can be obtained by querying the authorized certificate.

SAN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Subject Alternate Name (SAN), simply put, when multiple domain names are needed and used for various services, SAN certificates are often used. SAN allows a variety of values ​​to be associated with the certificate using the subjectAltName field in the security certificate. These values ​​are called subject alternative names.

Domain transfer vulnerability
----------------------------------------
DNS zone transfer refers to a redundant backup server using data from the primary server to refresh its own zone database. This is to prevent the main server from being unexpectedly unavailable from affecting the resolution of the entire domain name.

Generally speaking, domain transfer operations should only be initiated by trusted backup DNS servers, but if authorization is misconfigured, any user can obtain the domain name information of the entire DNS server. This misauthorization is called a DNS domain transfer vulnerability.

Passive DNS
----------------------------------------
Passive DNS passively records responses from different domain name servers from recursive domain name servers to form a database. Using the Passive DNS database, you can know which IPs the domain name has been bound to, which domain names the IP has been associated with, and the earliest/latest appearance time of the domain name, which provides great help for testing. Websites such as Virustotal, passivetotal, and CIRCL all provide Passive DNS database queries.

Pan-analysis
----------------------------------------
Pan-resolution is to resolve all A records of `*.example.com` to a certain IP address. This situation needs to be handled during subdomain enumeration to prevent a large number of invalid records from being generated.

important records
----------------------------------------

CNAME
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CNAME is Canonical name, also known as alias, which points a domain name to another domain name. It may contain information about other related businesses. The CDN acceleration function used by many websites takes advantage of this record.

MX records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The MX record is the Mail Exchanger, which records the server address corresponding to the domain name when sending emails. Can be used to find SMTP server information.

NS records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NS (Name Server) records are domain name server records, used to specify which DNS server to resolve domain names.

SPF record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SPF (Sender Policy Framework) is a DNS record type proposed to prevent spam. It is a TXT type record that is used to register all IP addresses owned by a domain name used to send outgoing emails. Relevant IP information can be obtained through SPF records. The commonly used command is ``dig example.com txt``.

CDN
----------------------------------------

CDN verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You can determine whether the target uses CDN by pinging from multiple places. Commonly used websites include ``http://ping.chinaz.com/`` ``https://asm.ca.com/en/ping.php``, etc.

Domain name search
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The parent domain or subdomain name of a domain name that uses CDN does not necessarily use CDN. You can find the corresponding IP in this way.

History search
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The CDN may have been launched after a period of time after the website was launched. You can find the real IP by searching domain name resolution records.

Email message
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Communicate via email through social engineering and obtain the IP address from the email header. The IP address may be the real IP of the website or the target's exit IP.

subdomain blasting
----------------------------------------
In environments such as intranets where the above techniques are not easy to use, or when you want to monitor the launch of new domain names, you can find valid domain names by trying them in batches.

Cache detection technology
----------------------------------------
In enterprise networks, DNS servers are usually configured to provide domain name resolution services for hosts in the network. Domain name cache snooping (DNS Cache Snooping) technology is to send domain name resolution requests to these servers, but does not require the use of recursive mode, to detect whether a certain domain name has been requested. This method can be used to detect whether certain software, especially security software, is used.
