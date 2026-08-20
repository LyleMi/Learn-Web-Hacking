SQL injection tips
================================

wide byte injection
--------------------------------
Generally, when programmers use gbk coding for development, they will use ``set names 'gbk'`` to set. This sentence is equivalent to

::

    set
    character_set_connection = 'gbk',
    character_set_result = 'gbk',
    character_set_client = 'gbk';

The vulnerability occurs because after executing ``set character_set_client = 'gbk';``, mysql will think that the data passed by the client is gbk encoded, and use gbk to decode, while mysql_real_escape is executed before decoding. But if you use ``set names 'gbk'`` directly, real_escape does not know the encoding of the set data, and will add ``%5c``. At this time, the server gets the data decoding and thinks that the submitted character +%5c is a character of gbk, which creates a vulnerability.

There are three solutions. The first is to set the client's charset to binary, so that no decoding operation is performed. The second method is ``mysql_set_charset('gbk')``, where the encoded information will be saved in the connection with the database, so this problem will not occur.
The third way is to use pdo.

There are some other coding techniques. For example, latin will discard invalid unicode, so admin%32 is not equal to admin in the code, but will be equal to admin in the database comparison.

secondary injection
--------------------------------
Second-Order SQL Injection is a special type of SQL injection attack. Similar to general SQL injection attacks, attackers will perform illegal operations by entering malicious SQL statements. Secondary SQL injection means that the attacker injects malicious data into the application and then waits for the application to store the data in the database. When the application reads this data from the database again, the malicious data will be read out and malicious operations will be performed.

For example, a web application might store user input in a database and then display it on subsequent pages. If an attacker injects malicious SQL statements into user input, these statements will be stored in the database. When the application reads these contents from the database and uses them in subsequent logic, malicious SQL statements may be executed, leading to a successful attack.

Compared with general SQL injection attacks, secondary SQL injection attacks are more difficult to prevent and detect because attackers do not directly send malicious SQL statements to the application, but store them in the database waiting for the application to read. Therefore, preventing secondary SQL injection attacks requires taking some special defensive measures, such as more stringent filtering and escaping of input data, the use of precompilation, etc.
