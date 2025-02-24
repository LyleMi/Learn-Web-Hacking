Precompiled
========================================

Introduction
----------------------------------------
SQL injection is caused by the interpreter performing incoming data as commands, and precompilation is a way to solve this problem. Unlike ordinary execution processes, precompiling a query is completed through two interactions. The template of the query statement is sent in the first interaction, and the SQL engine on the backend parses it into AST or Opcode, and the data is sent in the second interaction, and substituting in AST or Execute in Opcode. Because the syntax parsing has been completed at this time, there will be no process of obfuscating data and code.

Simulation precompilation
----------------------------------------
In order to prevent the low-version database from supporting precompilation, simulated precompilation will simulate the parameter binding process within the client and perform custom escapes.

Bypass
----------------------------------------

Precompilation usage error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Precompilation is only the part of the field value replaced by placeholders. If the command passed in for the first interaction uses string splicing, making the command controllable by the attacker, then precompilation will not take effect.

Some parameters are not precompiled
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In some cases, the database processing engine will check whether the data table and data columns exist, so the data table name and column name cannot be replaced by placeholders. In this case, if the table and column names are controllable, a vulnerability may be introduced.

Precompiled implementation error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some language engines have certain implementation problems and may have bypass vulnerabilities.
