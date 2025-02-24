Introduction
----------------------------------------
DNS is a simple request-response protocol, a distributed database that maps domain names and IP addresses to each other, which can make people more convenient to access the Internet. DNS uses port 53 of TCP and UDP protocols.

Request response
----------------------------------------

DNS records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- A
- Return the IPv4 address corresponding to the domain name
- AAAA
- NS
- Domain Name Server
- Return to which domain name server to resolve the domain name
- PTR
- Reverse Recording
- Records from IP address to domain name
- MX
- Email exchange history
- Record the IP address corresponding to the email domain name

Response code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- noeror

::

No error condition

- FORMERR

::

Format error - The name server was unable to interpret the query

- SERVFAIL

::

Server failure - The name server was unable to process this query due to a problem with the name server

- Nxdomain

::

this code signifies that the domain name referenced in the query does not exist

- NOTIMP

::

Not Implemented - The name server does not support the requested kind of query

- REFUSED

::

Refused - The name server refuses to perform the specified operation for policy reasons

- Nadata

::

A pseudo RCODE which indicates that the name is valid, for the given class, but [there] are no records of the given type A NODATA response has to be inferred from the answer.


How the domain name system works
----------------------------------------

Analytical process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DNS resolution process is recursively query, and the specific process is as follows:

- When a user wants to access the domain name www.example.com, first check whether the hosts are recorded or whether the machine has DNS cache. If so, the result will be returned directly. Otherwise, query the recursive server for the IP address of the domain name.
- When the recursive cache is empty, first query the root server for the IP address of the com top-level domain
- The root server informs the recursive server com the IP address of the top-level domain server
- Recursively query the com top-level domain server's IP of the authoritative server responsible for example.com
- com top-level domain server returns the corresponding IP address
- Recursively query the address record of www.example.com from the authoritative server of example.com
- Authoritative server informs www.example.com of the address record
- Recursive server returns query results to client

Domain delivery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DNS servers can be divided into primary servers, backup servers and cache servers. Domain transfer refers to the backup server copying data from the main server and updating its own database using the obtained data. Domain delivery is a mechanism for synchronizing databases between primary and secondary servers.

Server Type
----------------------------------------

Root Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The root server is the core of DNS, responsible for the resolution of the top-level domain names in the Internet, is used to maintain the authoritative information of the domain, and guide the DNS query to the corresponding domain name server.

The root server represents the top ``.`` domain in the domain name tree, and is generally omitted.

The domain names of 13 IPv4 root servers are a to m, that is, a.root-servers.org to m.root-servers.org. All servers store the same data and only contain the authoritative information of the TLD domain name approved by ICANN.

Authoritative Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The domain name zone file is stored on the authoritative server, and the authoritative information of the domain name within the domain is maintained. The recursive server can obtain resource records for DNS query from the authoritative server.

An authoritative server needs to be registered in the TLD management bureau to which the domain name it hosts belongs. The same authoritative server can host different TLD domain names, and there can also be multiple authoritative servers in the same domain.

Recursive server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The recursive server is responsible for receiving user query requests, performing recursive queries and responding to user query requests. Initially, the recursive server only records the Hint file with the root domain name.
