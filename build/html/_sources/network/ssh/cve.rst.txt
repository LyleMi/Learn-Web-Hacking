Related CVE
========================================

CVE-2018-15473
----------------------------------------
CVE-2018-15473 allows the client to obtain the username existing on the server through traversal. This vulnerability affects the version of OpenSSH <= 7.7.

CVE-2016-20012
----------------------------------------
CVE-2016-20012 allows clients to traverse whether the client can log in through a <user, public key> pair when only knowing the public key information.

Since the developers of OpenSSH believe that modifying the relevant authentication method requires increasing the frequency of client reading the private key, no corresponding repair is made.

For related discussions, please refer to this `PR <https://github.com/openssh/openssh-portable/pull/270>`_ .
