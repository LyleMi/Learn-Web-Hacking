Java
================================

反序列化
--------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的 ``ObjectOutputStream`` 类的 ``writeObject()`` 方法可以实现序列化，类 ``ObjectInputStream类的readObject()`` 方法用于反序列化。

如果要实现类的反序列化，则是对其实现 ``Serializable`` 接口。

相关函数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``ObjectInputStream.readObject``
- ``ObjectInputStream.readUnshared``
- ``XMLDecoder.readObject``
- ``Yaml.load``
- ``XStream.fromXML``
- ``ObjectMapper.readValue``
- ``JSON.parseObject``

存在危险的基础库
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``commons-fileupload 1.3.1``
- ``commons-io 2.4``
- ``commons-collections 3.1``
- ``commons-logging 1.2``
- ``commons-beanutils 1.9.2``
- ``org.slf4j:slf4j-api 1.7.21``
- ``com.mchange:mchange-commons-java 0.2.11``
- ``org.apache.commons:commons-collections 4.0``
- ``com.mchange:c3p0 0.9.5.2``
- ``org.beanshell:bsh 2.0b5``
- ``org.codehaus.groovy:groovy 2.3.9``
- ``org.springframework:spring-aop 4.1.4.RELEASE``

漏洞修复和防护
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 通过Hook resolveClass来校验反序列化的类
- 使用ValidatingObjectInputStream来校验反序列化的类

框架漏洞
--------------------------------

Struts 2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `CVE-2017-5638 <https://github.com/immunio/apache-struts2-CVE-2017-5638>`_
- `CVE-2017-9805 <https://github.com/mazen160/struts-pwn_CVE-2017-9805>`_
- `CVE-2017-12611 <https://github.com/brianwrf/S2-053-CVE-2017-12611>`_


Weblogic
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Weblogic漏洞CVE-2017-10271利用 <http://webcache.googleusercontent.com/search?q=cache%3AsH7j8TF8uOIJ%3Awww.freebuf.com%2Fvuls%2F160367.html>`_


参考链接
--------------------------------
- `Java反序列化漏洞从入门到深入 <https://mp.weixin.qq.com/s/nNTw3HMnkX63d9ybdx3USQ>`_
- `Java反序列化漏洞通用利用分析 <https://blog.chaitin.cn/2015-11-11_java_unserialize_rce/>`_
- `JRE8u20反序列化漏洞分析 <http://www.freebuf.com/vuls/176672.html>`_
- `Java Sandbox Escape <http://phrack.org/papers/escaping_the_java_sandbox.html>`_
