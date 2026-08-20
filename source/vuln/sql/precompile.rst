precompiled
========================================

Introduction
----------------------------------------
SQL injection is caused by the interpreter executing the incoming data as a command. Precompilation is a method used to solve this problem. Different from the ordinary execution process, pre-compilation completes a query through two interactions. The first interaction sends the template of the query statement, which is parsed into AST or Opcode by the back-end SQL engine. The second interaction sends the data and substitutes it into the AST or Opcode for execution. Because the syntax parsing has been completed at this time, there will no longer be a process of confusing data and code.

Simulate precompilation
----------------------------------------
In order to prevent low-version databases from not supporting precompilation, simulated precompilation will simulate the parameter binding process within the client and perform customized escaping.

bypass
----------------------------------------

Precompilation usage error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Precompilation only uses placeholders to replace the field values. If the command passed in for the first interaction uses string concatenation, making the command controllable by the attacker, then precompilation will not take effect.

Some parameters cannot be precompiled
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In some cases, the database processing engine will check whether the data table and data column exist, so the data table name and column name cannot be replaced by placeholders. In this case, if the table name and column name are controllable, vulnerabilities may be introduced.

Precompilation implementation error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some language engines have certain implementation problems and may have bypass vulnerabilities.
