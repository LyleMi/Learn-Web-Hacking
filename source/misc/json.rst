JSON
========================================
JSON (JavaScript Object Notation) is the cornerstone of communication in many data formats.

security risk
----------------------------------------
- Duplicate key ``{"test": 1, "test": 2}``
- Special key values ​​``\x00`` ``\x0d`` ``\ud800`` ``"`` etc.
- serialization
- specific numerical value
    - an integer exceeding the upper limit
    - Scientific notation
    - Different representations of null values

Reference link
----------------------------------------

Related specifications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 8259 The JavaScript Object Notation (JSON) Data Interchange Format <https://tools.ietf.org/html/rfc8259>`_
- `ECMA-404 The JSON data interchange syntax <https://www.ecma-international.org/publications-and-standards/standards/ecma-404/>`_
- `json5 <https://json5.org/>`_
