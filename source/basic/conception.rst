基础概念
================================

伪协议
--------------------------------

data伪协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

格式
``data:[<MIME-type>][;charset=<encoding>][;base64],data``

- 没指定MIME，浏览器会用``text/plain``替代
- 没制定charset，浏览器用``us-ascii``替代
- 没制定base64，则百分号编码


about伪协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
一般只有about:blank，返回零字节，其他的视浏览器不同而定

javascript/vbscript伪协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``<a href='javascript:foo()'></a>``


