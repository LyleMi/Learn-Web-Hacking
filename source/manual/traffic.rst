Traffic related
================================

TCPDump
--------------------------------
TCPDump is a data packet capture and analysis tool that can completely intercept the data packets transmitted in the network and provide analysis. It supports filtering for network layer, protocol, host, network or port and provides logical statements to filter packets.

Common command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-B <buffer_size>`` The buffer size for capturing traffic. If it is too small, packet loss may occur. The unit is KB.
- ``-c <count>`` Exit after grabbing n packages
- ``-C <file_size>`` After the currently recorded package exceeds a certain size, create a new file record in MB
- ``-i <interface>`` specifies to capture the traffic passing through the network card
- ``-n`` do not translate addresses
- ``-r <file>`` Read the saved pcap file
- ``-s <snaplen>`` intercepts snaplen bytes of data from each message, 0 means all data
- ``-q`` outputs brief protocol-related information, and the output lines are relatively short.
- ``-W <cnt>`` will no longer write after cnt files are filled.
- ``-w <file>`` Save traffic to file
    - When subcontracting by time, you can use strftime format naming, such as ``%Y_%m_%d_%H_%M_%S.pcap``
- ``-G <seconds>`` divide packets by time
- ``-v`` produces verbose output, ``-vv`` ``-vvv`` produces even more verbose output
- ``-X`` Output the message header and packet content
- ``-Z <user>`` Convert user before writing file

Bro
--------------------------------
Bro is an open source network traffic analysis tool that supports multiple protocols and can analyze traffic in real time or offline.

command line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Real-time monitoring ``bro -i <interface> <list of script to load>``
- Analyze local traffic ``bro -r <pcapfile> <scripts...>``
- Split the log after parsing the traffic ``bro-cut``

script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To be able to extend and customize Bro's functionality, Bro provides an event-driven scripting language.


tcpflow
--------------------------------
Tcpflow is also a packet capture tool. It is characterized by displaying data content in units of streams. When analyzing data from protocols such as HTTP, it will be more convenient to use tcpflow.

Common command line options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-b max_bytes`` defines the maximum crawl traffic
- ``-e name`` specifies the parsed scanner
- ``-i interface`` specifies the crawling interface
- ``-o outputdir`` specifies the output folder
- ``-r file`` Read file
- ``-R file`` Read the file, but only the complete file

tshark
--------------------------------
WireShark's command line tool can extract the data you want through commands, redirect it to a file, or combine it with an upper-layer language to call the command line to process the data.

Input interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-i <interface>`` specifies the capture interface, the default is the first non-local loop interface
- ``-f <capture filter>`` Set the packet capture filter expression and follow the libpcap filter syntax. This option is filtered during the packet capture process and is not used if local files are analyzed.
- ``-s <snaplen>`` Set the snapshot length, which is used to read the complete packet, because there is a limit of 65535 in network transmission, the value 0 represents the snapshot length 65535, the default is 65535
- ``-p`` works in non-mixed mode, that is, only cares about traffic related to the local machine
- ``-B <buffer size>`` Set the buffer size, only effective for windows, the default is 2M
- ``-y <link type>`` Set the data link layer protocol for packet capture. If not set, it defaults to the first protocol found by ``-L``
- ``-D`` prints a list of interfaces and exits
- ``-L`` lists the data link layer protocols supported by this machine for use with the -y parameter.
- ``-r <infile>`` Set to read local files

Capture stop options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-c <packet count>`` ends after capturing n packets. By default, unlimited captures are made.
- ``-a <autostop cond>``
    - ``duration:NUM`` stops capturing after num seconds
    - ``filesize:NUM`` stops capturing after numKB
    - ``files:NUM`` stops capturing after capturing num files

Processing options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-Y <display filter>`` uses read filter syntax, which can be used instead of the ``-R`` option in a single analysis
- ``-n`` disables name resolution for all addresses (default is to allow all)
- ``-N`` enables a certain layer of address name resolution. ``m`` represents the MAC layer, ``n`` represents the network layer, ``t`` represents the transport layer, and ``C`` represents the current asynchronous DNS lookup. If both the ``-n`` and ``-N`` arguments are present, ``-n`` will be ignored. If neither the ``-n`` nor the ``-N`` parameters are written, all address name resolution will be enabled by default.
- ``-d`` unpacks and outputs the specified data according to the relevant protocol. If you want to unpack the traffic of tcp 8888 port according to http, it should be written as ``-d tcp.port==8888,http``. You can use ``tshark -d`` to list all supported valid selectors.
　　
Output options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-w <outfile>`` Set the output file of raw data. stdout when not set
- ``-F <output file type>`` Set the output file format, the default is ``.pcapng``, use ``tshark -F`` to list all supported output file types
- ``-V`` increases detailed output
- ``-O <protocols>`` Display details only for protocols specified by this option
- ``-P`` prints summary information of the package even if the decoded results are written to a file
- ``-S <separator>`` line separator
- ``-x`` is set in the decoding output result, and the specific data is displayed in the form of HEX dump after each packet.
- ``-T pdml|ps|text|fields|psml`` Set the format of decoding result output, the default is text
- ``-e`` If the ``-T`` option is specified, ``-e`` is used to specify which fields to output
- ``-t a|ad|d|dd|e|r|u|ud`` Set the time format of the decoding result
- ``-u s|hms`` Format output seconds
- ``-l`` flush standard output after outputting each packet
- ``-q`` is used in conjunction with the ``-z`` option to perform statistical analysis
- ``-X <key>:<value>`` extension, lua_script, read_format
- ``-z`` statistics option, specific reference documentation
　　
Other options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-h`` displays command line help
- ``-v`` displays tshark version information

