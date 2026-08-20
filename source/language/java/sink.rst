Common sinks
========================================

Command execution/injection
----------------------------------------
- java.lang.Runtime.getRuntime().exec()
- java.lang.ProcessBuilder

XXE
----------------------------------------
- java.net.bull.javamelody.PayloadNameRequestWrapper
- javax.xml.bind.Unmarshaller
- javax.xml.parsers.DocumentBuilderFactory
- javax.xml.parsers.SAXParser
- javax.xml.stream.XMLStreamReader
- javax.xml.transform.sax.SAXSource
- javax.xml.transform.sax.SAXTransformerFactory
- javax.xml.transform.TransformerFactory
- javax.xml.validation.SchemaFactory
- javax.xml.validation.Validator
- javax.xml.xpath.XpathExpression
- org.apache.commons.digester3.Digester
- org.apache.ofbiz.base.util.UtilXml
- org.dom4j.io.SAXReader
- org.jdom.input.SAXBuilder
- org.jdom2.input.SAXBuilder
- org.xml.sax.helpers.XMLReaderFactory
- org.xml.sax.XMLReader

SSRF
----------------------------------------
- HttpClient.execute
- HttpClients.execute
- HttpURLConnection.getInputStream
- ImageIO.read
- OkHttpClient.newCall.execute
- Request.Get.execute
- Request.Post.execute
- URL.openStream
- URLConnection.getInputStream

Deserialization
----------------------------------------

Related Sink functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``JSON.parseObject``
- ``ObjectInputStream.readObject``
- ``ObjectInputStream.readUnshared``
- ``ObjectMapper.readValue``
- ``XMLDecoder.readObject``
- ``XStream.fromXML``
- ``Yaml.load``

Magic Call
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The following magic methods will be automatically called during the deserialization process.

- ``readObject``
- ``readExternal``
- ``readResolve``
- ``readObjectNoData``
- ``validateObject``
- ``finalize``

Mainstream JSON libraries
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Mainstream JSON libraries include Gson, Jackson, Fastjson, etc. Because JSON is often used in deserialization, related libraries have a greater impact.

Among them, Gson can only deserialize basic types by default. If it is a complex type, the programmer needs to implement the deserialization mechanism, which is relatively safe.

Jackson will not deserialize non-public properties unless @jsonAutoDetect is specified. When defending, you do not need to use the enableDefaultTyping method. Relevant CVEs include CVE-2017-7525 and CVE-2017-15095.

FastJson is Alibaba's open source JSON parsing library. It supports serialization of Java Beans into JSON strings and deserialization from JSON strings to Java Beans. Related CVEs include CVE-2017-18349, etc.

Common sink points in FastJson are:

- ``JSON.toJSONString``
- ``JSON.parseObject``
- ``JSON.parse``
