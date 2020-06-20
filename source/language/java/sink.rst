常见Sink
========================================

命令执行/注入
----------------------------------------
- java.lang.Runtime.getRuntime().exec()
- java.lang.ProcessBuilder

XXE
----------------------------------------
- javax.xml.parsers.DocumentBuilderFactory
- javax.xml.parsers.SAXParser
- javax.xml.transform.TransformerFactory
- javax.xml.validation.Validator
- javax.xml.validation.SchemaFactory
- javax.xml.transform.sax.SAXTransformerFactory
- javax.xml.transform.sax.SAXSource
- org.xml.sax.XMLReader
- org.xml.sax.helpers.XMLReaderFactory
- org.dom4j.io.SAXReader
- org.jdom.input.SAXBuilder
- org.jdom2.input.SAXBuilder
- javax.xml.bind.Unmarshaller
- javax.xml.xpath.XpathExpression
- javax.xml.stream.XMLStreamReader
- org.apache.commons.digester3.Digester

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

反序列化
----------------------------------------

相关Sink函数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``ObjectInputStream.readObject``
- ``ObjectInputStream.readUnshared``
- ``XMLDecoder.readObject``
- ``Yaml.load``
- ``XStream.fromXML``
- ``ObjectMapper.readValue``
- ``JSON.parseObject``

Magic Call
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
以下的魔术方法都会在反序列化过程中被自动的调用。

- ``readObject``
- ``readExternal``
- ``readResolve``
- ``readObjectNoData``
- ``validateObject``
- ``finalize``

主流JSON库
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
主流的JSON库有Gson、Jackson、Fastjson等，因为JSON常在反序列化中使用，所以相关库都有较大的影响。

其中Gson默认只能反序列化基本类型，如果是复杂类型，需要程序员实现反序列化机制，相对比较安全。

Jackson除非指明@jsonAutoDetect，Jackson不会反序列化非public属性。在防御时，可以不使用enableDefaultTyping方法。相关CVE有CVE-2017-7525、CVE-2017-15095。

FastJson是阿里巴巴的开源JSON解析库，支持将Java Bean序列化为JSON字符串，也支持从JSON字符串反序列化到Java Bean，相关CVE有CVE-2017-18349等。

FastJson常见的Sink点有：

- ``JSON.toJSONString``
- ``JSON.parseObject``
- ``JSON.parse``
