NTLM authentication
========================================

NTLM certification
----------------------------------------
NTLM is the abbreviation of NT LAN Manager. NTLM is a challenge/response-based authentication protocol and is the standard security protocol in early versions of Windows NT.

Basic process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The client locally encrypts the current user's password into a password hash
- The client sends the account number in clear text to the server
- The server generates a 16-bit random number and sends it to the client as a challenge
- The client encrypts the challenge with the encrypted password hash and returns it to the server as a response
- The server sends the user name, challenge, and response to the domain controller
- The domain controller uses this username to find the user's password hash in the SAM password management repository, and then uses this password hash to encrypt the chellenge
- The domain controller compares the two encrypted challenges. If they are the same, the authentication succeeds, otherwise the authentication fails.

Net-NTLMv1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The basic process of Net-NTLMv1 protocol is as follows:

- The client sends a request to the server
- After receiving the request, the server generates an 8-bit Challenge and sends it back to the client.
- After the client receives the Challenge, it encrypts the Challenge using the password hash of the logged in user and sends it to the server as a response.
- Server verification response

The calculation method of Net-NTLMv1 response is

- Divide the user's NTLM hash with zeros to 21 bytes into three groups of 7-byte data
- The three sets of data are used as three sets of keys for the 3DES encryption algorithm to encrypt the Challenge sent by the Server.

This method is relatively fragile and can be cracked based on packet capture tools and rainbow table blasting tools.

Net-NTLMv2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Since Windows Vista, Microsoft has used the Net-NTLMv2 protocol by default. The basic process is as follows:

- The client sends a request to the server
- After receiving the request, the server generates a 16-bit Challenge and sends it back to the client.
- After the client receives the Challenge, it encrypts the Challenge using the password hash of the logged in user and sends it to the server as a response.
- Server verification response

Hash
----------------------------------------

LM Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LM Hash (LAN Manager Hash) is the earliest encryption algorithm used in Windows and was designed by IBM. LM Hash uses DES with hard-coded keys and is flawed. Early Windows systems such as XP, Server 2003, etc. used LM Hash, and later systems disabled LM Hash by default and used NTLM Hash.

The calculation method of LM Hash is:

- Convert user's password to uppercase, truncated at 14 bytes
- If it is less than 14 bytes, you need to add 0×00 after it.
- Divide 14 bytes into two 7-byte passwords
- Use ``KGS!@#$%`` as the secret key to DES encrypt these two sets of data to obtain a 16-byte hash
- Get the final LM Hash after splicing.

As an early algorithm, LM Hash has many problems:

- Password length cannot exceed 14 characters and is not case sensitive
- If the password length is less than 7 characters, the value of the latter set of hashes can be determined by ending with ``aad3b435b51404ee`` to determine that the password length does not exceed 7 characters.
- Block encryption greatly reduces the complexity of passwords
- DES algorithm is low in intensity

NTLM Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to solve the security problem of LM Hash, Microsoft introduced the NTLM protocol in Windows NT 3.1 in 1993.

Windows 2000/XP/2003 uses LM Hash before the password exceeds 14 characters, and uses NTLM Hash after the password exceeds 14 characters. Later versions starting with Vista all use NTLM Hash.

The calculation method of NTLM Hash is:

- Convert the password to hexadecimal and encode it in Unicode
- Calculate hash value based on MD4

attack
----------------------------------------

Pass The Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Pass The Hash (PtH) is a way for attackers to capture the account login credentials and then reuse the credentials Hash to carry out attacks.

Microsoft released defense guidance against Pass The Hash attacks in December 2012. The article mentioned some defense methods and explained why it did not provide updated patches for Pass The Hash.

Pass The Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In an environment where NTLM is disabled, you can use tools such as mimikatz to directly obtain the password.

NTLM Relay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When an attacker can control the client network to a certain extent, he or she can use a man-in-the-middle attack to gain permissions. Pretend to be an authentication server to the client, and pretend to be a client requiring authentication to the server.

Reference link
----------------------------------------
- `Windows identity authentication and utilization ideas <https://www.freebuf.com/articles/system/224171.html>`_
- `The NTLM Authentication Protocol and Security Support Provider <http://davenport.sourceforge.net/ntlm.html>`_
