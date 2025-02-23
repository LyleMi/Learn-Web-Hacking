SQLMap usage
================================

Install ``git clone https://github.com/sqlmaproject/sqlmap.git sqlmap``

Common parameters
--------------------------------

- ``-u`` ``--url`` Specify the target url
- ``-m`` Get multiple target scans from text
- ``-r`` Load HTTP request from file
- ``--data`` Submit data in POST
- ``-random-agent`` Random ua
- ``--user-agent`` specifies ua
- ``--delay`` Sets the delay between requests
- ``--timeout`` Specify the timeout
- ``--dbms`` specifies db. The dbs supported by sqlmap include MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, SQLite, etc.
- ``--os`` Specify the database server operating system
- ``--tamper`` Specify tamper
- ``--level`` Specify the detection level
- ``--risk`` Specify risk level
- ``--technique`` Injection technology
- B: Boolean-based blind SQL injection
- E: Error-based SQL injection
- U: UNION query SQL injection
- S: Stacked queries SQL injection
- T: Time-based blind SQL injection


Tamper Quick Check
--------------------------------

================================            ========================
Script Name Function
================================            ========================
apostrophemask.py replaces quotes with utf8
equaltolike.py like instead of equals
space2dash.py bypass filtering '=' Replace space character ("), ('' - ') followed by a dash comment, a random string and a new line ('
')
greatest.py bypass filtering '>' , replace the greater than sign with GREATEST.
space2hash.py replaces space with # number random string and line break
apostrophenullencode.py bypasses filtering double quotes, replacing characters and double quotes.
halfversionedmorekeywords.py Bypass the firewall when the database is mysql, add mysql version comment before each keyword
space2morehash.py replaces space with # and more random strings newline characters
appendnullbyte.py loads zero-byte character encoding at the end of payload
ifnull2ifisnull.py bypasses filtering on IFNULL. Replace like 'IFNULL(A, B)' to 'IF(ISNULL(A), B, A)'
space2mssqlblank.py replaces space with other empty symbols
base64encode.py replaces base64 encoding
space2mssqlhash.py replaces space
modsecurityversioned.py filters spaces, containing full query version comments
space2mysqlblank.py space replaces other whitespace symbols (mysql)
between.py replaces the greater than sign with between (>)
space2mysqldash.py replaces space character (")(' - ') followed by a dash comment a new line (' n')
multiplespaces.py add multiple spaces around SQL keywords
space2plus.py replaces space with +
bluecoat.py SQL statement replaced with a valid random whitespace character after SQL statement. Then replace = like
nonrecursivereplacement.py replaces predefined SQL keyword with suitable for replacement (e.g. .replace("SELECT", "")) filters
space2randomblank.py replaces space characters ("") from a valid set of optional characters for a random whitespace character
sp_password.py appends sp_password' from the end of the automatic fuzzing payload of DBMS log
chardoubleencode.py double url encoding (not processed to encode)
unionalltounion.py replace UNION ALL SELECT UNION SELECT
charencode.py url encoding
randomcase.py random case
unmagicquotes.py wide character bypass GPC addslashes
randomcomments.py splits sql keywords with ``/**/``
charunicodeencode.py string unicode encoding
securesphere.py appends special string
versionedmorekeywords.py comment bypass
space2comment.py                            Replaces space character ``' '`` with comments ``/**/``
================================            ========================
