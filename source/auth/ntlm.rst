NTLM Authentication
========================================

NTLM certification
----------------------------------------
NTLM is the abbreviation of NT LAN Manager, which is a challenge/response authentication protocol and is a standard security protocol in earlier versions of Windows NT.

Basic Process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The client encrypts the current user's password locally to become a password hash
- The client sends an account to the server explicitly
- The server generates a random number of 16-bits to send to the client as a challenge
- The client uses the encrypted password hash to encrypt the challenge, and then returns it to the server as a response
- Server side sends username, challenge, and response to the domain controller
- The domain controller uses this username to find the password hash of this user in the SAM password management library, and then uses this password hash to encrypt the chestenge
- Domain controller compares the two-time encryption challenge. If the same is true, the authentication will be successful, otherwise the authentication will fail.

Non-ntlmv1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The basic process of the Net-NTLMv1 protocol is as follows:

- The client sends a request to the server
- After the server receives the request, it generates an 8-bit Challenge and sends it back to the client
- After the client receives the Challenge, it uses the password hash of the logged in user to encrypt the Challenge and sends it to the server as a response
- Server verification response

The calculation method of Net-NTLMv1 response is

- Divide the user's NTLM hash to zero to 21 bytes into three groups of 7 bytes of data
- Three sets of data are used as three sets of keys of the 3DES encryption algorithm, encrypting the Challenge sent by the Server

This method is relatively fragile and can be cracked based on packet capture tools and rainbow table blasting tools.

Net-NTLMv2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Since Windows Vista, Microsoft has used the Net-NTLMv2 protocol by default, and its basic process is as follows:

- The client sends a request to the server
- After the server receives the request, it generates a 16-bit Challenge and sends it back to the client
- After the client receives the Challenge, it uses the password hash of the logged in user to encrypt the Challenge and sends it to the server as a response
- Server verification response

Hash
----------------------------------------

LM Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
LM Hash (LAN Manager Hash) is the earliest encryption algorithm used in Windows and designed by IBM. LM Hash uses DES with hard-coded keys and has flaws. Early Windows systems such as XP, Server 2003, etc. used LM Hash, while later systems disabled LM Hash by default and used NTLM Hash.

The calculation method of LM Hash is:

- Convert user's password to capital, 14 byte truncation
- If you need to add 0×00 to make up for less than 14 bytes
- Divide 14 bytes into two 7 bytes passwords
- DES encryption of these two sets of data with ``KGS!@#$%`` as the key to obtain a 16-byte hash
- Get the final LM Hash after splicing.

As an early algorithm, LM Hash has many problems:

- Password length will not exceed 14 characters and is case-insensitive
- If the password length is less than 7 digits, the value of the latter set of hashs is determined. You can judge that the password length does not exceed 7 digits by the ending of ``aad3b435b51404ee``
- Packet encryption greatly reduces password complexity
- Low DES algorithm strength

NTLM Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to solve the security issues of LM Hash, Microsoft introduced the NTLM protocol in Windows NT 3.1 in 1993.

Windows 2000/XP/2003 Use LM Hash before the password exceeds 14 digits and NTLM Hash after the password exceeds 14 digits. Later, all versions starting with Vista use NTLM Hash.

The calculation method of NTLM Hash is:

- Convert password to hexadecimal and encode Unicode
- Calculate hash value based on MD4

attack
----------------------------------------

Pass The Hash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Pass The Hash (PtH) is a way for an attacker to capture the account login credentials and reuse the credentials Hash to attack.

Microsoft released defense guidance for Pass The Hash attacks in December 2012, which mentioned some defense methods and explained why update patches are not provided for Pass The Hash.

Pass The Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In an environment where NTLM is disabled, you can use mimikatz and other tools to get the password directly.

NTLM Relay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When an attacker can control the client network to a certain extent, he can use the man-in-the-middle attack to obtain permissions. The client is disguised as an authentication server, and the server is disguised as a client that needs authentication.

Reference link
----------------------------------------
- `Windows identity authentication and utilization ideas <https://www.freebuf.com/articles/system/224171.html>`_
- `The NTLM Authentication Protocol and Security Support Provider <http://davenport.sourceforge.net/ntlm.html>`_
