Java
================================

反序列化
--------------------------------
序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的ObjectOutputStream类的writeObject()方法可以实现序列化，类ObjectInputStream类的readObject()方法用于反序列化。

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
- `Java反序列化漏洞通用利用分析 <https://blog.chaitin.cn/2015-11-11_java_unserialize_rce/>`_