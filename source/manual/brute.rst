Blasting tools
================================

Hydra
--------------------------------
- ``-R`` continue to crack from the last progress
- ``-S`` link with SSL
- ``-s<PORT>`` Specify the port
- ``-l<LOGIN>`` Specify the cracked user
- ``-L<FILE>`` Specify user name dictionary
- ``-p<PASS>`` Specify password cracking
- ``-P<FILE>`` Specify password dictionary
- ``-e<ns>`` optional option, n: empty password test, s: use the specified user and password test
- ``-C<FILE>`` Use colon split format, such as "user:pwd" instead of the -L/-P parameter
- ``-M<FILE>`` Specify one line of target list file
- ``-o<FILE>`` Specify the result output file
- ``-f`` After using the -M parameter, the cracking is aborted when the first pair of login names or passwords is found.
- ``-t<TASKS>`` The number of threads running simultaneously, default is 16
- ``-w<TIME>`` Set the maximum timeout, unit of seconds, the default is 30s
- ``-vV`` display detailed process
