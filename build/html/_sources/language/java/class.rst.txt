kind
========================================

life cycle
----------------------------------------
Overall, the life cycle of a class in Java is as follows: Loading -> [Linking: Verification -> Preparation -> Resolutin] -> Initialization -> Use (Using) -> Unloading.

The loading process is divided into three steps:

- Get a binary byte stream that defines this class by fully qualified class name
- Convert the static storage structure represented by the byte stream into the runtime data structure of the method area
- Generate ``java.lang.Class`` object representing this class in memory, as an access portal for various data in this class in the method area

The verification phase is mainly used to ensure that the byte stream of the Class file meets the requirements of the current virtual machine, and is divided into several steps:

- Determine file format: whether it starts with ``0xCAFEBABE``, whether the primary and secondary version numbers are within the processing range
- Metadata Verification
- Bytecode verification
- Symbol Reference Verification
