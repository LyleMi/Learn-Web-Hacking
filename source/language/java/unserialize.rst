反序列化
========================================

简介
----------------------------------------
序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的 ``ObjectOutputStream`` 类的 ``writeObject()`` 方法可以实现序列化，类 ``ObjectInputStream类的readObject()`` 方法用于反序列化。

如果要实现类的反序列化，则是对其实现 ``Serializable`` 接口。

相关函数
----------------------------------------
- ``ObjectInputStream.readObject``
- ``ObjectInputStream.readUnshared``
- ``XMLDecoder.readObject``
- ``Yaml.load``
- ``XStream.fromXML``
- ``ObjectMapper.readValue``
- ``JSON.parseObject``

主流JSON库
----------------------------------------

GSON
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gson默认只能反序列化基本类型，如果是复杂类型，需要程序员实现反序列化机制，相对比较安全。

Jackson
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
除非指明@jsonAutoDetect，Jackson不会反序列化非public属性。在防御时，可以不使用enableDefaultTyping方法。

相关CVE有

- CVE-2017-7525
- CVE-2017-15095

Fastjson
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
相关CVE有

- CVE-2017-18349

存在危险的基础库
----------------------------------------
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
----------------------------------------

Hook resolveClass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在使用 ``readObject()`` 反序列化时会调用 ``resolveClass`` 方法读取反序列化的类名，可以通过hook该方法来校验反序列化的类，一个Demo如下

::

    @Override
    protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
        if (!desc.getName().equals(SerialObject.class.getName())) {
            throw new InvalidClassException(
                    "Unauthorized deserialization attempt",
                    desc.getName());
        }
        return super.resolveClass(desc);
    }

以上的Demo就只允许序列化 ``SerialObject`` ，通过这种方式，就可以设置允许序列化的白名单

ValidatingObjectInputStream
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Apache Commons IO Serialization包中的 ``ValidatingObjectInputStream`` 类提供了 ``accept`` 方法，可以通过该方法来实现反序列化类白/黑名单控制，一个demo如下

::

    private static Object deserialize(byte[] buffer) throws IOException, ClassNotFoundException , ConfigurationException {
        Object obj;
        ByteArrayInputStream bais = new ByteArrayInputStream(buffer);
        ValidatingObjectInputStream ois = new ValidatingObjectInputStream(bais); 
        ois.accept(SerialObject.class);
        obj = ois.readObject();
        return obj;
    }

ObjectInputFilter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Java 9提供了支持序列化数据过滤的新特性，可以继承 ``java.io.ObjectInputFilter`` 类重写 ``checkInput`` 方法来实现自定义的过滤器，并使用 ``ObjectInputStream`` 对象的 ``setObjectInputFilter`` 设置过滤器来实现反序列化类白/黑名单控制。
