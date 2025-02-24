DNS utilization
----------------------------------------

DGA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DGA (Domain Generate Algorithm) is a technical method that uses random characters to generate C&C domain names to evade domain name blacklist detection, which is commonly found in botnet. Generally speaking, the survival time of a DGA domain name is about 1-7 days.

During communication, both the client and the server run the same set of DGA algorithm to generate the same alternative domain name list. When an attack is required, select a small number of them to register to establish communication and can apply rapid changes to the registered domain name. IP technology, quickly change IP, so that both domain names and IP can be changed quickly.

There are many ways to generate DGA domain names, which can be divided into determinism and uncertainty generation according to seed type. The seeds of uncertainty may use some instant data of the day, such as exchange rate information.

DNS tunnel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The DNS tunnel tool encapsulates other protocol traffic into the tunnel into the DNS protocol and transmits it on the tunnel. These data packets are decapsulated when they exit the tunnel to restore the data.
