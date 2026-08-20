SQLMap usage
================================

Install ``git clone https://github.com/sqlmapproject/sqlmap.git sqlmap``

Common parameters
--------------------------------

- ``-u`` ``--url`` specifies the target url
- ``-m`` Get multiple target scans from text
- ``-r`` Load HTTP requests from file
- ``--data`` Submit data in POST mode
- ``-random-agent`` random ua
- ``--user-agent`` specifies ua
- ``--delay`` Set the delay between requests
- ``--timeout`` specifies the timeout period
- ``--dbms`` specifies the db. The dbs supported by sqlmap include MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, SQLite, etc.
- ``--os`` specifies the database server operating system
- ``--tamper`` specifies tamper
- ``--level`` specifies the detection level
- ``--risk`` specifies the risk level
- ``--technique`` injection technology
    - B: Boolean-based blind SQL injection
    - E: Error-based SQL injection
    - U: UNION query SQL injection
    - S: Stacked queries SQL injection
    - T: Time-based blind SQL injection


Tamper Quick Facts
--------------------------------

================================            ========================
Script name Function
================================            ========================
apostrophemask.py replaces quotes with utf8
equaltolike.py like replaces the equal sign
space2dash.py bypasses filtering '=' by replacing space characters ("), ('' - ') followed by a dash comment, a random string and a new line ('\n')
greatest.py bypasses filtering '>' and replaces the greater than sign with GREATEST.
space2hash.py replaces spaces with # signs, random strings and newline characters
apostrophenullencode.py bypasses filtering double quotes, replacement characters and double quotes.
halfversionedmorekeywords.py Bypass the firewall when the database is mysql, add a mysql version comment before each keyword
space2morehash.py replaces spaces with # signs and more random strings and newline characters
appendnullbyte.py loads zero-byte character encoding at end of payload
ifnull2ifisnull.py bypasses IFNULL filtering. Replace something like 'IFNULL(A, B)' with 'IF(ISNULL(A), B, A)'
space2mssqlblank.py replaces spaces with other empty symbols
base64encode.py replace with base64 encoding
space2mssqlhash.py replaces spaces
modsecurityversioned.py filters spaces and contains complete query version comments
space2mysqlblank.py spaces replace other whitespace symbols (mysql)
between.py replaces the greater than sign (>) with between
space2mysqldash.py replaces the space character (") (' - ') followed by a dash comment with a new line (' n')
multiplespaces.py adds multiple spaces around SQL keywords
space2plus.py replaces spaces with +
bluecoat.py replaces the space character after the SQL statement with a valid random white space character. Then replace = with like
nonrecursivereplacement.py replaces predefined SQL keywords with suitable for replacement (such as .replace("SELECT", "")) filters
space2randomblank.py replaces the space character ("") with a random whitespace character from a valid set of optional characters
sp_password.py appends sp_password' to the end of the payload for automatic obfuscation from the DBMS log
chardoubleencode.py double url encoding (does not process encoding)
unionalltounion.py replaces UNION ALL SELECT UNION SELECT
charencode.py url encoding
randomcase.py random case
unmagicquotes.py wide character bypass GPC addslashes
randomcomments.py uses ``/**/`` to split sql keywords
charunicodeencode.py string unicode encoding
securesphere.py appends specially crafted strings
versionedmorekeywords.py comment bypass
space2comment.py                            Replaces space character ``' '`` with comments ``/**/``
================================            ========================
