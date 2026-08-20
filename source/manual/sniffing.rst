sniffing tool
================================

Nmap
--------------------------------
``nmap [<scan type>...] [<options>] {<scan target description>}``

Specify goals
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CIDR style ``192.168.1.0/24``
- Comma separated ``www.baidu.com,www.zhihu.com``
- Dividing line ``10.22-25.43.32``
- from file ``-iL <inputfile>``
- Exclude unnecessary hosts ``--exclude <host1 [, host2] [, host3] ... >`` ``--excludefile <excludefile>``

host discovery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sL`` List Scan - simply list targets to scan
- ``-sn/-sP`` Ping Scan - disable port scan
- ``-Pn`` Treat all hosts as online -- skip host discovery
- ``-sS/sT/sA/sW/sM`` TCP SYN/Connect()/ACK/Window/Maimon scans
- ``-sU`` UDP Scan
- ``-sN/sF/sX`` TCP Null, FIN, and Xmas scans

.. list-table:: Scan mode table
   :widths: 15 15 25 25 20
   :header-rows: 1

   * - name
     - package tags
     - Port OPEN
     - port CLOSE
     - Features
   * - TCP SYN scan
     - SYN
     - Reply ACK+SYN
     - Reply to RST
     - The application has no logs but is easily discoverable
   * - full connection scan
     - SYN
     - Reply ACK+SYN
     - Reply to RST
     - easy to spot
   * - ACK scan
     - ACK
     - Reply to RST
     - Packet is dropped
     - .
   * - FIN scan
     - FIN
     - Packet is dropped
     - Reply to RST
     - Need to wait for timeout, low efficiency
   * - TCP Xmas scan
     - FIN+URG+PSH
     - Packet is dropped
     - Reply to RST
     - Need to wait for timeout, low efficiency; not applicable to all operating systems
   * - TCP NULL scan
     - NULL
     - Packet is dropped
     - Reply to RST
     - Need to wait for timeout, low efficiency; not applicable to all operating systems

port scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--scanflags`` Customized TCP scanning
- ``-P0`` no ping
- ``PS [port list]`` (TCP SYN ping) // need root on Unix
- ``PA [port list]`` (TCP ACK ping)
- ``PU [port list]`` (UDP ping)
- ``PR (Arp ping)``
- ``p <port message>``
- ``F`` fast scan
- ``r`` does not use random order scanning

Service and version detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sV`` version detection
- ``--allports`` do not exclude any ports for version detection
- ``--version-intensity <intensity>`` Set version scan intensity
- ``--version-light`` Turn on lightweight mode // Level 2
- ``--version-all`` try every probe // level 9
- ``--version-trace`` Track version scanning activity
- ``-sR RPC`` scan

Operating system scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-O`` enables operating system detection
- ``--osscan-limit`` Perform operating system detection for the specified target
- ``--osscan-guess``
- ``--fuzzy`` specifies operating system detection results

time and performance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Adjust the size of parallel scan groups
    - ``--min-hostgroup<milliseconds>``
    - ``--max-hostgroup<milliseconds>``
- Adjust the parallelism of detection messages
    - ``--min-parallelism<milliseconds>``
    - ``--max-parallelism<milliseconds>``
- Adjust detection packet timeout
    - ``--min_rtt_timeout <milliseconds>``
    - ``--max-rtt-timeout <milliseconds>``
    - ``--initial-rtt-timeout <milliseconds>``
- Abandon slow target hosts
    - ``--host-timeout<milliseconds>``
- Adjust the time interval of detection messages
    - ``--scan-delay<milliseconds>``
    - ``--max_scan-delay<milliseconds>``
- Set time template
    - ``-T <Paranoid|Sneaky|Polite|Normal|Aggressive|Insane>``
    - ``-T<0-5>`` (the bigger, the faster)

Related to evading detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-f`` message segmentation
- ``--mtu`` use the specified MTU
- ``-D<decoy1[, decoy2][, ME], ...>`` Use decoy covert scanning
- ``-S<IP_Address>`` source address spoofing
- ``-e <interface>`` Use the specified interface
- ``--source-port<portnumber>;-g<portnumber>`` Source port spoofing
- ``--data-length<number>`` append random data when sending a message
- ``--ttl <value>`` Set ttl
- ``--randomize-hosts`` randomizes the order of target hosts
- ``--spoof-mac<macaddress, prefix, orvendorname>`` MAC address spoofing

output
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-oN<filespec>`` standard output
- ``-oX<filespec>`` XML output
- ``-oS<filespec>`` ScRipTKIdd|3oUTpuT
- ``-oG<filespec>`` Grep output
- ``-oA<basename>`` Output to all formats
- ``--open`` only outputs possible open port information

Details and debugging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-v`` information verbosity
- ``-d [level]`` debug level
- ``--packet-trace`` trace sent and received packets
- ``--iflist`` List interfaces and routes

Masscan
--------------------------------

compile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: bash

    sudo apt-get install git gcc make libpcap-dev
    git clone https://github.com/robertdavidgraham/masscan
    cd masscan
    make -j

Command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--ports`` specifies the port range
- ``--rate`` specifies the rate
- ``--source-ip`` specifies the source IP
