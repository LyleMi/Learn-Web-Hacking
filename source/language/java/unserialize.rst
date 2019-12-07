反序列化
========================================

简介
----------------------------------------
序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的 ``ObjectOutputStream`` 类的 ``writeObject()`` 方法可以实现序列化，类 ``ObjectInputStream类的readObject()`` 方法用于反序列化。

如果要实现类的反序列化，则是对其实现 ``Serializable`` 接口。

序列数据结构
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ ``0xaced`` 魔术头

序列化流程
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ ObjectOutputStream实例初始化时，将魔术头和版本号写入bout （BlockDataOutputStream类型） 中
+ 调用ObjectOutputStream.writeObject()开始写对象数据
    + ObjectStreamClass.lookup()封装待序列化的类描述 （返回ObjectStreamClass类型） ，获取包括类名、自定义serialVersionUID、可序列化字段 （返回ObjectStreamField类型） 和构造方法，以及writeObject、readObject方法等
    + writeOrdinaryObject()写入对象数据
        + 写入对象类型标识
        + writeClassDesc()进入分支writeNonProxyDesc()写入类描述数据
            + 写入类描述符标识
            + 写入类名
            + 写入SUID （当SUID为空时，会进行计算并赋值）
            + 计算并写入序列化属性标志位
            + 写入字段信息数据
            + 写入Block Data结束标识
            + 写入父类描述数据
        + writeSerialData()写入对象的序列化数据
            + 若类自定义了writeObject()，则调用该方法写对象，否则调用defaultWriteFields()写入对象的字段数据 （若是非原始类型，则递归处理子对象）

反序列化流程
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ ObjectInputStream实例初始化时，读取魔术头和版本号进行校验
+ 调用ObjectInputStream.readObject()开始读对象数据
    + 读取对象类型标识
    + readOrdinaryObject()读取数据对象
        + readClassDesc()读取类描述数据
            + 读取类描述符标识，进入分支readNonProxyDesc()
            + 读取类名
            + 读取SUID
            + 读取并分解序列化属性标志位
            + 读取字段信息数据
            + resolveClass()根据类名获取待反序列化的类的Class对象，如果获取失败，则抛出ClassNotFoundException
            + skipCustomData()循环读取字节直到Block Data结束标识为止
            + 读取父类描述数据
            + initNonProxy()中判断对象与本地对象的SUID和类名 （不含包名） 是否相同，若不同，则抛出InvalidClassException
        + ObjectStreamClass.newInstance()获取并调用离对象最近的非Serializable的父类的无参构造方法 （若不存在，则返回null） 创建对象实例
        + readSerialData()读取对象的序列化数据
            + 若类自定义了readObject()，则调用该方法读对象，否则调用defaultReadFields()读取并填充对象的字段数据

Sink
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

主流JSON库
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
主流的JSON库有Gson、Jackson、Fastjson等，因为JSON常在反序列化中使用，所以相关库都有较大的影响。

其中Gson默认只能反序列化基本类型，如果是复杂类型，需要程序员实现反序列化机制，相对比较安全。

Jackson除非指明@jsonAutoDetect，Jackson不会反序列化非public属性。在防御时，可以不使用enableDefaultTyping方法。相关CVE有CVE-2017-7525、CVE-2017-15095。

Fastjson相关CVE有CVE-2017-18349。

漏洞利用
----------------------------------------

存在危险的基础库
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
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
