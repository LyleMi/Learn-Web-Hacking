code obfuscation
========================================

There are many solutions for PHP code obfuscation, including encrypted files, obfuscation, virtual machine-based encryption, opcode-based encryption, extension-based encryption, etc.

Encrypted files refer to directly encrypting all PHP files, decrypting them in a specific way and then executing them through eval and other methods. This method is the easiest to restore. Obfuscation is a method of removing variable names and changing the code organization to a certain extent through AST to reduce code readability. This method can be partially restored through corresponding reverse substitution. Based on the virtual machine method, I implemented a virtual machine myself and converted PHP into specific code. This method is basically impossible to restore but the execution efficiency is very low. Encryption based on opcode is a method used by tools such as zend guard. The code is compiled into opcode and then executed. Extension-based encryption requires the introduction of additional extensions to implement operations such as adding junk code, modifying control flow, and encrypting plaintext strings.
