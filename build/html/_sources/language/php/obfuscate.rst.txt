Code obfuscation
========================================

There are many solutions for PHP code obfuscation, including encrypted files, obfuscation, virtual machine-based encryption, opcode-based encryption, extended encryption, etc.

Encrypted files refer to directly encrypting all php files, decrypting them through specific methods and executing them through eval, etc. This method is most easily restored. Obfuscation is a method of removing variable names and changing the code organization to a certain extent through AST to reduce the readability of the code. This method can be partially restored through corresponding reverse substitution. I implemented a virtual machine by myself based on a virtual machine, converting PHP into specific code. This method is basically impossible to restore but the execution efficiency is very low. Opcode encryption is a method used by tools such as Zend Guard. Compile the code into opcode and then execute it. Extension-based encryption requires the introduction of additional extensions to implement operations such as adding junk code, modifying control flow, encrypting plaintext strings, etc.
