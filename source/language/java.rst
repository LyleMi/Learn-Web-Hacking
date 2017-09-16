Java
================================

反序列化
-------------------------------


序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的ObjectOutputStream类的writeObject()方法可以实现序列化，类ObjectInputStream类的readObject()方法用于反序列化。

https://blog.chaitin.cn/2015-11-11_java_unserialize_rce/