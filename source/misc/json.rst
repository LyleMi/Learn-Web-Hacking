JSON
========================================
JSON (JavaScript Object Notation) 是许多数据格式通信的基石。

安全风险
----------------------------------------
- 重复的key ``{"test": 1, "test": 2}``
- 特殊的key值 ``\x00`` ``\x0d`` ``\ud800`` ``"`` 等
- 序列化
- 特定的数值
    - 超过上限的整数
    - 科学计数法
    - null值的不同表示

参考链接
----------------------------------------

相关规范
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 8259 The JavaScript Object Notation (JSON) Data Interchange Format <https://tools.ietf.org/html/rfc8259>`_
- `ECMA-404 The JSON data interchange syntax <https://www.ecma-international.org/publications-and-standards/standards/ecma-404/>`_
- `json5 <https://json5.org/>`_
