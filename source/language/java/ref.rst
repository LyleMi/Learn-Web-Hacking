参考链接
========================================

官方文档
----------------------------------------
- `ognl <http://commons.apache.org/proper/commons-ognl/>`_
- `Java SE Security Guide <https://docs.oracle.com/javase/9/security/toc.htm>`_
- `Java RMI Release Notes for JDK 6 <https://docs.oracle.com/javase/7/docs/technotes/guides/rmi/relnotes.html>`_
- `Java Release Notes for JDK 7 <https://www.oracle.com/technetwork/java/javase/7u21-relnotes-1932873.html>`_

机制说明
----------------------------------------
- `深入理解Java类加载 <https://www.cnblogs.com/czwbig/p/11127222.html>`_

反序列化
----------------------------------------

标准
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Java序列化【草案一】 <https://blog.csdn.net/silentbalanceyh/article/details/8183849>`_
- `Java 14 Object Serialization Specification <https://docs.oracle.com/en/java/javase/14/docs/specs/serialization/index.html>`_

利用与技巧
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Marshalling Pickles how deserializing objects can ruin your day <https://www.slideshare.net/frohoff1/appseccali-2015-marshalling-pickles>`_
- `AppSecCali 2015: Marshalling Pickles <https://frohoff.github.io/appseccali-marshalling-pickles/>`_
- `More serialization hacks with AnnotationInvocationHandler <http://wouter.coekaerts.be/2015/annotationinvocationhandler>`_
- `Pure JRE 8 RCE Deserialization gadget <https://github.com/pwntester/JRE8u20_RCE_Gadget>`_
- `Breaking Defensive Serialization <http://slightlyrandombrokenthoughts.blogspot.com/2010/08/breaking-defensive-serialization.html>`_
- `Java反序列化漏洞从入门到深入 <https://mp.weixin.qq.com/s/nNTw3HMnkX63d9ybdx3USQ>`_
- `Java反序列化漏洞通用利用分析 <https://blog.chaitin.cn/2015-11-11_java_unserialize_rce/>`_
- `JRE8u20反序列化漏洞分析 <http://www.freebuf.com/vuls/176672.html>`_
- `浅析Java序列化和反序列化 <https://xz.aliyun.com/t/3847>`_
- `Commons Collections Java反序列化漏洞深入分析 <https://security.tencent.com/index.php/blog/msg/97>`_
- `FAR SIDES OF JAVA REMOTE PROTOCOLS <https://i.blackhat.com/eu-19/Wednesday/eu-19-An-Far-Sides-Of-Java-Remote-Protocols.pdf>`_
- `JDK8u20反序列化漏洞新型PoC思路及具体实现 <https://mp.weixin.qq.com/s/3bJ668GVb39nT0NDVD-3IA>`_
- `Pwn a CTF Platform with Java JRMP Gadget <http://blog.orange.tw/2018/03/pwn-ctf-platform-with-java-jrmp-gadget.html>`_
- `漫谈 JEP 290 <https://nosec.org/home/detail/4846.html>`_

框架
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `WebLogic反序列化漏洞漫谈 <https://www.freebuf.com/articles/web/169770.html>`_
- `从WebLogic看反序列化漏洞的利用与防御 <https://cert.360.cn/report/detail?id=c8eed4b36fe8b19c585a1817b5f10b9e>`_
- `JSON反序列化之殇 <https://github.com/shengqi158/fastjson-remote-code-execute-poc/blob/master/Java_JSON%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B9%8B%E6%AE%87_%E7%9C%8B%E9%9B%AA%E5%AE%89%E5%85%A8%E5%BC%80%E5%8F%91%E8%80%85%E5%B3%B0%E4%BC%9A.pdf>`_
- `Shiro组件漏洞与攻击链分析 <https://mp.weixin.qq.com/s/j_gx9C_xL1LyrnuFFPFsfg>`_
- `Application Security With Apache Shiro <https://www.infoq.com/articles/apache-shiro/>`_
- `Shiro安全框架【快速入门】 <https://zhuanlan.zhihu.com/p/54176956>`_
- `Shiro 实战(四) - 过滤器机制 <https://cloud.tencent.com/developer/article/1367702>`_

沙箱
----------------------------------------
- `Java Sandbox Escape <http://phrack.org/papers/escaping_the_java_sandbox.html>`_

框架
----------------------------------------
- `Struts <https://github.com/apache/struts>`_
- `Struts Examples <https://github.com/apache/struts-examples>`_
- `Eclipse Jetty <https://github.com/eclipse/jetty.project>`_
- `SpringBootVulExploit <https://github.com/LandGrey/SpringBootVulExploit>`_ SpringBoot 相关漏洞学习资料，利用方法和技巧合集，黑盒安全评估 checklist

框架利用技巧
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Spring Boot Fat Jar 写文件漏洞到稳定 RCE 的探索 <https://landgrey.me/blog/22/>`_

RMI
----------------------------------------
- `Java RMI与RPC的区别 <https://www.cnblogs.com/ygj0930/p/6542811.html>`_
- `Remote Method Invocation (RMI) <https://www.oreilly.com/library/view/learning-java/1565927184/ch11s04.html>`_
- `Java 中 RMI、JNDI、LADP、JRMP、JMX、JMS那些事儿 <https://paper.seebug.org/1091>`_
- `Oracle: Developing T3 Clients <http://docs.oracle.com/cd/E11035_01/wls100/client/t3.html>`_

JNDI
----------------------------------------
- `Overview of JNDI <https://docs.oracle.com/javase/tutorial/jndi/overview/index.html>`_
- `关于 JNDI 注入 <https://paper.seebug.org/417/>`_
- `A Journey From JNDI LDAP Manipulation To RCE <https://www.blackhat.com/docs/us-16/materials/us-16-Munoz-A-Journey-From-JNDI-LDAP-Manipulation-To-RCE.pdf>`_
- `如何绕过高版本JDK的限制进行JNDI注入 <https://www.freebuf.com/column/207439.html>`_

WebShell
----------------------------------------
- `各种姿势jsp webshell <https://xz.aliyun.com/t/7798>`_

其他漏洞
----------------------------------------
- `JAVA常见的XXE漏洞写法和防御 <blog.spoock.com/2018/10/23/java-xxe/index.html>`_
