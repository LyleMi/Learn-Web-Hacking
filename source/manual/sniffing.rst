Sniffing Tool
================================

Nmap
--------------------------------
``nmap [<scan type>...] [<option>] {<scan target description>}``

Specify the target
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CIDR style ``192.168.1.0/24``
- Comma splitting ``www.baidu.com,www.zhihu.com``
- Dividing line ``10.22-25.43.32``
- From file ``-iL <inputfile>```
- Exclude unwanted host ``--exclude <host1 [, host2] [, host3] ... >`` ``--excludefile <excludefile>``

Host Discovery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sL`` List Scan - simply list targets to scan
- ``-sn/-sP`` Ping Scan - disable port scan
- ``-Pn`` Treat all hosts as online -- skip host discovery
- ``-sS/sT/sA/sW/sM`` TCP SYN/Connect()/ACK/Window/Maimon scans
- ``-sU`` UDP Scan
- ``-sN/sF/sX`` TCP Null, FIN, and Xmas scans

.. list-table:: Scan the method table
:widths: 15 15 25 25 20
:header-rows: 1

* - Name
- Package tags
- Port OPEN
- Port CLOSE
- Features
* - TCP SYN scan
- SYN
- Reply ACK+SYN
- Reply to RST
- The application has no logs, but is easily discovered
* - Full connection scan
- SYN
- Reply ACK+SYN
- Reply to RST
- Easy to be discovered
* - ACK scan
- ACK
- Reply to RST
- The bag is discarded
- .
* - FIN scan
- FIN
- The bag is discarded
- Reply to RST
- Need to wait for timeout, low efficiency
* - TCP Xmas Scan
- FIN+URG+PSH
- The bag is discarded
- Reply to RST
- Need to wait for timeout, inefficient; not applicable to all operating systems
* - TCP NULL Scan
- NULL
- The bag is discarded
- Reply to RST
- Need to wait for timeout, inefficient; not applicable to all operating systems

Port Scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--scanflags`` Customized TCP scanning
- ``-P0`` without ping
- ``PS [port list]`` (TCP SYN ping) // need root on Unix
- ``PA [port list]`` (TCP ACK ping)
- ``PU [port list]`` (UDP ping)
- ``PR (Arp ping)``
- ``p <port message>``
- ``F`` Quick Scan
- ``r`` does not use random order scans

Service and version detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sV`` version detection
- ``--allports`` does not exclude any ports for version detection
- ``--version-intensity <intensity>`` Set version scan intensity
- ``--version-light`` Turn on lightweight mode // Level 2
- ``--version-all`` Try each probe // Level 9
- ``--version-trace`` Tracking version scanning activity
- ``-sR RPC`` scan

Operating system scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-O`` Enable operating system detection
- ``--osscan-limit`` performs operating system detection for specified targets
- ``--osscan-guess``
- ``--fuzzy`` speculate on the operating system detection results

Time and performance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Resize the parallel scan group
- ``--min-hostgroup<milliseconds>``
- ``--max-hostgroup<milliseconds>``
- Adjust the parallelism of the detection packets
- ``--min-parallelism<milliseconds>``
- ``--max-parallelism<milliseconds>``
- Adjust the detection message timeout
- ``--min_rtt_timeout <milliseconds>``
- ``--max-rtt-timeout <milliseconds>``
- ``--initial-rtt-timeout <milliseconds>``
- Give up low-speed target host
- ``--host-timeout<milliseconds>``
- Adjust the time interval of the detection message
- ``--scan-delay<milliseconds>``
- ``--max_scan-delay<milliseconds>``
- Set time template
- ``-T <Paranoid|Sneaky|Polite|Normal|Aggressive|Insane>``
- ``-T<0-5>`` (The bigger the faster)

Escape detection related
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-f`` message segmentation
- ``--mtu`` Use the specified MTU
- ``-D<decoy1[, decoy2][, ME], ...>`` Use bait to conceal scan
- ``-S<IP_Address>`` Source address coaxing
- ``-e <interface>`` Use the specified interface
- ``--source-port<portnumber>;-g<portnumber>`` Source port coaxing
- ``--data-length<number>`` Attach random data when sending a message
- ``--ttl <value>`` Set ttl
- ``--randomize-hosts`` Random order of target hosts
- ``--spoof-mac<macaddress, prefix, orvendorname>`` MAC address coaxing

Output
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-oN<filespec>`` standard output
- ``-oX<filespec>`` XML output
- ``-oS<filespec>`` ScRipTKIdd|3oUTpuT
- ``-oG<filespec>`` Grep output
- ``-oA<basename>`` output to all formats
- ``--open`` only outputs possible open port information

Details and debugging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-v`` information detail
- ``-d [level]`` debug level
- ``--packet-trace`` Tracking of sent and received messages
- ``--iflist`` List interfaces and routes

Masscan
--------------------------------

Compilation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: bash

sudo apt-get install git gcc make libpcap-dev
git clone https://github.com/robertdavidgraham/masscan
cd masscan
make -j

Command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--ports`` Specify the port range
- ``--rate`` Specify the rate
- ``--source-ip`` Specify the source IP
