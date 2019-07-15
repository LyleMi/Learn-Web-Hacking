SQL注入小技巧
================================

宽字节注入
--------------------------------
一般程序员用gbk编码做开发的时候，会用 ``set names 'gbk'`` 来设定，这句话等同于

::

    set
    character_set_connection = 'gbk',
    character_set_result = 'gbk',
    character_set_client = 'gbk';

漏洞发生的原因是执行了 ``set character_set_client = 'gbk';`` 之后，mysql就会认为客户端传过来的数据是gbk编码的，从而使用gbk去解码，而mysql_real_escape是在解码前执行的。但是直接用 ``set names 'gbk'`` 的话real_escape是不知道设置的数据的编码的，就会加 ``%5c`` 。此时server拿到数据解码  就认为提交的字符+%5c是gbk的一个字符，这样就产生漏洞了。

解决的办法有三种，第一种是把client的charset设置为binary，就不会做一次解码的操作。第二种是是 ``mysql_set_charset('gbk')`` ，这里就会把编码的信息保存在和数据库的连接里面，就不会出现这个问题了。
第三种就是用pdo。

还有一些其他的编码技巧，比如latin会弃掉无效的unicode，那么admin%32在代码里面不等于admin，在数据库比较会等于admin。
