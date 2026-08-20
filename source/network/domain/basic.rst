Introduction
----------------------------------------
DNS is a simple request-response protocol. It is a distributed database that maps domain names and IP addresses to each other, making it easier for people to access the Internet. DNS uses port 53 of the TCP and UDP protocols.

request response
----------------------------------------

DNS records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- A
- Returns the IPv4 address corresponding to the domain name
- AAAA
- NS
- Domain name server
- Returns which domain name server resolves the domain name
- PTR
- Reverse recording
- Records from IP address to domain name
- MX
- Records of email exchanges
- Record the IP address corresponding to the email domain name

response code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- NOERROR

::

    No error condition

- FORMERR

::

    Format error - The name server was unable to interpret the query

- SERVFAIL

::

    Server failure - The name server was unable to process this query due to a problem with the name server

- NXDOMAIN

::

    this code signifies that the domain name referenced in the query does not exist

- NOTIMP

::

    Not Implemented - The name server does not support the requested kind of query

- REFUSED

::

    Refused - The name server refuses to perform the specified operation for policy reasons

- NODATA

::

    A pseudo RCODE which indicates that the name is valid, for the given class, but [there] are no records of the given type A NODATA response has to be inferred from the answer.


How the domain name system works
----------------------------------------

parsing process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DNS resolution process is a recursive query. The specific process is as follows:

- When a user wants to access the domain name www.example.com, he first checks whether the local hosts have a record or whether the local machine has a DNS cache. If so, the result is returned directly. Otherwise, the recursive server is queried for the IP address of the domain name.
- When the recursive cache is empty, first query the root server for the IP address of the com top-level domain
- The root server tells the recursive server the IP address of the com top-level domain name server
- Recursively query the com top-level domain name server for the IP of the authoritative server responsible for example.com
- The com top-level domain name server returns the corresponding IP address
- Recursively query the authoritative server of example.com for the address record of www.example.com
- The authoritative server informs the address record of www.example.com
- The recursive server returns query results to the client

domain transfer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS servers can be divided into main servers, backup servers and cache servers. Domain transfer means that the backup server copies data from the primary server and updates its own database with the obtained data. Domain transfer is a mechanism for synchronizing databases between primary and secondary servers.

Server type
----------------------------------------

root server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The root server is the core of DNS and is responsible for the resolution of the Internet's top-level domain names, maintaining the authoritative information of the domain, and guiding DNS queries to the corresponding domain name servers.

The root server represents the top-level ``.`` domain in the domain name tree and is generally omitted.

The domain name labels of the 13 IPv4 root servers are a to m, that is, a.root-servers.org to m.root-servers.org. The data stored by all servers is the same and only contains authoritative information of TLD domain names approved by ICANN.

authoritative server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Domain name Zone files are stored on the authoritative server to maintain authoritative information of domain names in the domain. The recursive server can obtain resource records for DNS queries from the authoritative server.

Authoritative servers need to be registered with the TLD management authority to which the domain name they host belongs. The same authoritative server can host different TLD domain names, and the same domain can also have multiple authoritative servers.

recursive server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The recursive server is responsible for receiving user query requests, conducting recursive queries and responding to user query requests. At the beginning, the recursive server only records the Hint file of the root domain name.
