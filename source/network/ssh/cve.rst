Related CVEs
========================================

CVE-2018-15473
----------------------------------------
CVE-2018-15473 allows the client to obtain the user name that exists on the server through traversal. This vulnerability affects OpenSSH <= 7.7.

CVE-2016-20012
----------------------------------------
CVE-2016-20012 allows a client to traverse via SSH_MSG_USERAUTH_REQUEST when only the public key information is known. Whether the client can log in via a certain <user, public key> pair.

Since the developers of OpenSSH believe that modifying the relevant authentication methods will require increasing the frequency of the client reading the private key, there is no corresponding fix.

For related discussions, please refer to this `PR <https://github.com/openssh/openssh-portable/pull/270>`_.
