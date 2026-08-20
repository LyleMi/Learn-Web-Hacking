DNS utilization
----------------------------------------

DGA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DGA (Domain Generate Algorithm) is a technical means that uses random characters to generate C&C domain names to evade domain name blacklist detection. It is common in botnets. Generally speaking, the survival time of a DGA domain name is about 1-7 days.

During communication, both the client and the server run the same set of DGA algorithms to generate the same list of alternative domain names. When it is necessary to launch an attack, a small number of them are selected for registration, and communication can be established. Rapid-changing IP technology can be applied to the registered domain names to quickly change IPs, so that both domain names and IPs can change quickly.

There are many ways to generate DGA domain names, which can be divided into deterministic and uncertain generation according to the seed type. The seeds of uncertainty may use some real-time data of the day, such as exchange rate information.

DNS tunnel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DNS tunnel tool encapsulates other protocol traffic entering the tunnel into the DNS protocol and transmits it over the tunnel. These data packets are decapsulated when they exit the tunnel and the data is restored.
