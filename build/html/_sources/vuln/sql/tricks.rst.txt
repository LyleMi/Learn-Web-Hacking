SQL injection tips
================================

Wide byte injection
--------------------------------
When programmers use gbk encoding for development, they will use ``set names 'gbk'`` to set it, which is equivalent to

::

set
character_set_connection = 'gbk',
character_set_result = 'gbk',
character_set_client = 'gbk';

The reason for the vulnerability is that after executing ``set character_set_client = 'gbk';``, mysql will think that the data transmitted by the client is gbk encoded, so use gbk to decode, while mysql_real_escape is executed before decoding. However, if you use ``set names 'gbk'`` directly, real_escape does not know the encoding of the set data, and will add ``%5c``. At this time, the server gets the data decoding and believes that the submitted character +%5c is a character of gbk, which creates a vulnerability.

There are three solutions. The first is to set the client's charset to binary, so that you will not perform a decoding operation. The second type is ``mysql_set_charset('gbk')``, where the encoded information will be saved in the connection with the database, and this problem will not occur.
The third type is to use pdo.

There are some other coding techniques, such as latin will discard invalid unicode, so admin%32 does not equal admin in the code, but in the database, it will equal admin.

Secondary injection
--------------------------------
Second-Order SQL Injection is a special type of SQL injection attack. Similar to the general SQL injection attack, an attacker will perform illegal operations by entering malicious SQL statements. Secondary SQL injection refers to an attacker injecting malicious data into the application and then waiting for the application to store the data in the database. When the application reads this data from the database again, the malicious data will be read out and malicious operations will be performed.

For example, a web application might store content entered by the user in a database and then display it on subsequent pages. If an attacker injects malicious SQL statements into user input, the statements are stored in the database. When an application reads these contents from the database and uses them in subsequent logic, malicious SQL statements may be executed, resulting in successful attacks.

Compared with general SQL injection attacks, secondary SQL injection attacks are more difficult to prevent and detect, because the attacker does not directly send malicious SQL statements to the application, but stores them in the database for the application to read. Therefore, preventing secondary SQL injection attacks requires some special defense measures, such as stricter filtering and escape processing of input data, and the use of precompilation.
