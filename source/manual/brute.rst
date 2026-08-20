blasting tools
================================

Hydra
--------------------------------
- ``-R`` Continue cracking from the last progress
- ``-S`` Use SSL link
- ``-s<PORT>`` specifies the port
- ``-l<LOGIN>`` specifies the user to crack
- ``-L<FILE>`` specifies user name dictionary
- ``-p<PASS>`` specifies password cracking
- ``-P<FILE>`` specifies password dictionary
- ``-e<ns>`` Optional options, n: empty password test, s: use the specified user and password test
- ``-C<FILE>`` Use colon-separated format, such as "user:pwd" instead of -L/-P parameters
- ``-M<FILE>`` specifies the target list file one line per line
- ``-o<FILE>`` specifies the result output file
- ``-f`` After using the -M parameter, stop cracking when the first pair of login names or passwords is found.
- ``-t<TASKS>`` Number of threads running simultaneously, the default is 16
- ``-w<TIME>`` Set the maximum timeout in seconds, the default is 30s
- ``-vV`` displays detailed process
