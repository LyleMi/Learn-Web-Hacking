kind
========================================

life cycle
----------------------------------------
Overall, the life cycle of a class in Java is as follows: Loading -> [Linking: Verification -> Preparation -> Resolutin] -> Initialization -> Using -> Unloading.

The loading process is divided into three steps:

- Get the binary byte stream that defines this class by its fully qualified class name
- Convert the static storage structure represented by the byte stream into the runtime data structure of the method area
- Generate a ``java.lang.Class`` object representing this class in memory as an access entry for various data of this class in the method area

The verification phase is mainly used to ensure that the byte stream of the Class file meets the requirements of the current virtual machine, and is divided into several steps:

- Determine the file format: whether it starts with ``0xCAFEBABE`` and whether the major and minor version numbers are within the processing range
- Metadata validation
- Bytecode verification
- Symbol reference verification
