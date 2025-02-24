Traffic related
================================

TCPDump
--------------------------------
TCPDump is a packet capture and analysis tool that can completely intercept data packets transmitted on the network to provide analysis. It supports filtering for network layer, protocol, host, network or port, and provides logical statements to filter packets.

Common command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-B <buffer_size>`` The buffer size of the crawling traffic. If it is too small, packet loss may be lost. The unit is KB
- ``-c <count>`` crawl n packets and exit
- ``-C <file_size>`` After the current record packet exceeds a certain size, another file record will be generated, in MB
- ``-i <interface>`` Specify the traffic passing through the network card
- ``-n`` does not convert address
- ``-r <file>`` Read the saved pcap file
- ``-s <snaplen>`` intercepts snapplen bytes from each message, 0 is all data
- ``-q`` outputs simple protocol-related information, and the output lines are relatively short.
- ``-W <cnt>`` No more writing after writing cnt files
- ``-w <file>`` Save traffic to file
- When subcontracting by time, you can use strftime's format to name, such as ``%Y_%m_%d_%H_%M_%S.pcap``
- ``-G <seconds>`` subcontract by time
- ``-v`` produces detailed output, ``-vv`````-vvv`` produces more detailed output
- ``-X`` outputs the contents of the message header and packet
- ``-Z <user>`` convert user before writing a file

Bro
--------------------------------
Bro is an open source network traffic analysis tool that supports multiple protocols and can analyze traffic in real time or offline.

Command line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Real-time monitoring ``bro -i <interface> <list of script to load>``
- Analyze local traffic ``bro -r <pcapfile> <scripts...>``
- Split and parsed logs ``bro-cut``

Script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to be able to extend and customize Bro's functionality, Bro provides an event-driven scripting language.


tcpflow
--------------------------------
tcpflow is also a packet capture tool. Its characteristic is to display data content in units of streams. When analyzing data from HTTP and other protocols, using tcpflow will be more convenient.

Common command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-b max_bytes`` defines the maximum crawling traffic
- ``-e name`` specifies the parsed scanner
- ``-i interface`` specifies the crawling interface
- ``-o outputdir`` Specify the output folder
- ``-r file`` Read file
- ``-R file`` reads the file, but only the complete file

Tshark
--------------------------------
WireShark's command line tool can extract the data you want through commands, redirect it to a file, or call the command line in combination with the upper-level language to realize the processing of data.

Input interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-i <interface>`` specifies the capture interface, default is the first non-local loop interface
- ``-f <capture filter>`` Set the packet capture filter expression, following the libpcap filter syntax. This option is filtered during the packet capture process. If you analyze local files, it will not be used.
- ``-s <snaplen>`` Set the snapshot length to read the complete packet, because there is a limit of 65535 for transmission in the network, and the value 0 represents the snapshot length 65535, which is default to 65535.
- ``-p`` works in non-mixed mode, that is, only care about traffic related to the unit
- ``-B <buffer size>`` Set the buffer size, only effective for windows, default is 2M
- ``-y <link type>`` Sets the data link layer protocol for packet capture, and if not set, the default is the first protocol found in ``-L``
- ``-D`` Print the list of interfaces and exit
- ``-L`` Lists the data link layer protocols supported by the machine for use with the -y parameter.
- ``-r <infile>`` Set to read local files

Capture Stop Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-c <packet count>`` ends after capturing n packets, and the default capture of infinite packets
- ``-a <autostop cond>``
- ``duration:NUM`` stops capturing after num seconds
- ``filesize:NUM`` stops capture after numKB
- ``files:NUM`` Stop capturing after capturing num files

Processing options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-Y <display filter>``` Use the syntax of read filters, which can be replaced with the ``-R`` option in a single analysis
- ``-n`` Prohibits all address name resolution (default is allowed)
- ``-N`` Enable address name resolution of a certain layer. ``m`` represents the MAC layer, ``n`` represents the network layer, ``t`` represents the transport layer, and ``C`` represents the current asynchronous DNS lookup. If the ``-n`` and ``-N`` parameters exist at the same time, ``-n`` will be ignored. If neither ``-n`` and ``-N`` parameters are written, all address name resolution is turned on by default.
- ``-d`` Unpack the specified data according to the relevant protocol. If you want to unpack the traffic on the tcp 8888 port as http, it should be written as ``-d tcp.port==8888,http``. Available ``tshark -d`` lists all supported valid selectors.
　　
Output options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-w <outfile>`` Sets the output file of raw data. stdout when not set
- ``-F <output file type>`` Set the output file format, the default is ``.pcapng``, and use ``tshark -F`` to list all supported output file types
- ``-V`` Add details output
- ``-O <protocols>`` Shows only the details of the protocol specified by this option
- ``-P`` Print the package summary information even if the decoding result is written into a file
- ``-S <separator>`` line splitter
- ``-x`` is set in the decoding output result, and the specific data is displayed in the HEX dump after each packet.
- ``-T pdml|ps|text|fields|psml`` Set the format of the decoding result output, default to text
- ``-e`` If the ``-T`` option is specified, ``-e`` is used to specify which fields to output
- ``-t a|ad|d|dd|e|r|u|ud`` Set the time format of the decoding result
- ``-u s|hms`` Format output seconds
- ``-l`` flush standard output after outputting each package
- ``-q`` combined with the ``-z`` option for statistical analysis
- ``-X <key>:<value>`` extension, lua_script, read_format
- ``-z`` Statistical options, specific reference documents
　　
Other options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-h`` Show command line help
- ``-v`` Shows tshark version information

