SQL注入
================================

SQL注入的目的
--------------------------------
1. 有账号体系的
    1. 无密码登录
    2. 获取密码
2. 获取数据库结构
3. 获取数据库，系统版本
4. 读写文件

注入分类
--------------------------------

SQL注入类型分为

1. 布尔盲注
2. 报错注入
3. union注入
4. 堆叠注入
5. 时间盲注

共计3类

1. inband

    a) 利用web应用来直接获取数据 
    b) 如Error-based SQL injection和Error-based SQL injection
    c) 都是通过web的响应或者错误反馈来提取数据

2. inference

    0) 通过web的一些反映来推断数据 
    1) 如Boolean-based blind SQL injection和Stacked queries SQL injection 
    2) 也就是我们通俗的盲注，
    3) 通过web应用的其他改变来推断数据
3. out of band(OOB)

    a) 通过其他传输方式来获得数据，比如DNS解析协议和电子邮件 

注入过程
--------------------------------
1. 判断注入点
    '
    and 1=1
    and 1=2
    or 1=1
    or 1=2
    and 1=23

2. 若存在注入点,判断数据库类型
    and exists (select * from msysobjects ) > 0 //access数据库

    and exists (select * from sysobjects ) > 0 //SQLServer数据库

3. 判断数据库表
    and exsits (select * from admin)


审计时看什么
--------------------------------
1. 看全局过滤能否bypass
2. 看是否有直接执行sql的地方
3. 看是用的什么驱动，mysql/mysqli/pdo
    1. 如果使用PDO，看是否是直接执行的地方


Fuzz
--------------------------------
- 注入常用函数与字符
- 测试注入
- 注释符
- 版本、主机名、用户名、库名
- 表和字段
    - 确定字段数
        - Order By
        - Select Into
    - 表名、列名
- 字符串连接
- 条件语句、时间函数
- 文件操作
- 带外通道
- fuzz出可能的过滤模式
    - 比如是否有trunc
    - 是否过滤某个字符
    - 是否过滤关键字
    - slash和编码


常用Bypass
--------------------------------
1. 编码绕过
    - 大小写
    - url编码
    - html编码
    - 十六进制编码
    - unicode编码
2. 注释
    - ++
    - \/\*\*\/
    - 内联注释用的更多，它有一个特性/!**/只有MySQL能识别
    - 代替空格
3. 只过滤了一次
4. 相同功能替换
    4.1 函数替换
        - substring 用mid sub
        - ascii 用hex bin
        - benchmark用 sleep
    4.2 变量替换
        - user() @@user
    4.3 符号和关键字
        - and &
        - or |
5. HTTP参数
    - HTTP参数污染
    - HTTP分割注入
6. 缓冲区溢出
    - 利用一些C语言的WAF，没有缓冲区保护
7. 利用本身参数


获取哪些信息
--------------------------------
表名

::

    union select table_name,2,3,4 from information_schema.tables where table_schema = database()

写文件

::

    union select 1,1,1 into outfile '/asddasdasdxzvt.txt'

读文件

::

    select @@datadir
    select load_file('databasename/tablename.MYD')


常用Payload
--------------------------------
::

    ascii(subtring(str,pos,length)) & 32 == 1

::

    报错注入
    select count(*),(floor(rand(0)*2))x from information_schema.tables group by x;

NoSQL注入
--------------------------------
TODO


SQL注入小技巧
--------------------------------

双查询注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
TODO

宽字节注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
一般程序员用gbk编码做开发的时候
会用
::

    set names 'gbk'

来设定
然后这句话等同于

::

    set
    character_set_connection = 'gbk',
    character_set_result = 'gbk',
    character_set_client = 'gbk';

漏洞发生的主要原因是因为set character_set_client = 'gbk';
因为执行了这句话之后，mysql就会认为客户端传过来的数据是gbk的，就会用gbk去解码
然后mysql_real_escape是在解码前执行的
但是直接用set names 'gbk'的话 real_escape是不知道设置的数据的编码的，就会直接加个%5c
那server拿到数据一解码  就认为提交的字符+%5c是gbk的一个字符，这样就产生漏洞了

那解决的办法就有三种
第一种是把client的charset设置为binary，就不会做一次解码的操作
第二种是是mysql_set_charset('gbk'),这里就会把编码的信息保存在和数据库的连接里面，就不会出现这个问题了
第三种就是用pdo

还有一些其他的编码技巧，比如latin会弃掉无效的unicode，那么admin%32在代码里面不等于admin，在数据库比较会等于admin