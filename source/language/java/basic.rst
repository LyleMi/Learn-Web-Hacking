基本概念
========================================

JVM
----------------------------------------
JVM是Java平台的核心，以机器代码来实现，为程序执行提供了所需的所有基本功能，例如字节码解析器、JIT编译器、垃圾收集器等。由于它是机器代码实现的，其同样受到二进制文件受到的攻击。

JCL是JVM自带的一个标准库，含有数百个系统类。默认情况下，所有系统类都是可信任的，且拥有所有的特权。

JDK
----------------------------------------
Java开发工具包(Java Development Kit，JDK)是Oracle公司发布的Java平台，有标准版(Standard Edition，Java SE)、企业版(Enterprise Edition，Java EE)等版本。

在最开始，JDK以二进制形式发布，而后在2006年11月17日，Sun以GPL许可证发布了Java的源代码，于是之后出现了OpenJDK。

JMX
----------------------------------------
JMX(Java Management Extensions，Java管理扩展)是一个为应用程序植入管理功能的框架，主要为管理和监视应用程序、系统对象、设备和面向服务的网络提供相应的工具。JMX可以远程读取系统中的值、调用系统中的方法。在JMX未配置身份验证或JDK版本过低存在反序列化漏洞时，可能会导致远程代码执行。

JNI
----------------------------------------
JNI (Java Native Interface) 是Java提供的和其他语言交互的接口。

JNA
----------------------------------------
JNA (Java Native Access) 是在JNI上的框架，用于自动实现Java接口到native function的映射，而不需要另外编写JNI代码。

OGNL
----------------------------------------
OGNL(Object-Graph Navigation Language，对象导航语言)是一种功能强大的表达式语言，通过简单一致的表达式语法，提供了存取对象的任意属性、调用对象的方法、遍历整个对象的结构图、实现字段类型转化等功能。

Struts2中使用了OGNL，提供了一个ValueStack类。ValueStack分为root和context两部分。root中是当前的action对象，context中是ActionContext里面所有的内容。

IO模型
----------------------------------------
Java 对操作系统的各种 IO 模型进行了封装，形成了不同的API。

BIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
BIO (Blocking I/O) 是同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成。

NIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NIO (New I/O) 是一种同步非阻塞的I/O模型，在Java 1.4中引入，对应 java.nio 包，提供了 Channel , Selector，Buffer等抽象。

AIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AIO (Asynchronous I/O) 在 Java 7 中引入，是NIO的改进版，是异步非阻塞的IO模型，基于事件和回调机制实现。

反射
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Java反射机制是指在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能被称为语言的反射机制。

相关类
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
================          ===================
类名                        用途
================          ===================
Class                       类的实体
Field                       类的成员变量
Method                      类的方法
Constructor                 类的构造方法
================          ===================

Class相关
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- asSubclass(Class<U> clazz)
    - 把传递的类的对象转换成代表其子类的对象
- Cast
    - 把对象转换成代表类或是接口的对象
- getClassLoader()
    - 获得类的加载器
- getClasses()
    - 返回一个数组，数组中包含该类中所有公共类和接口类的对象
- getDeclaredClasses()
    - 返回一个数组，数组中包含该类中所有类和接口类的对象
- forName(String className)
    - 根据类名返回类的对象
- getName()
    - 获得类的完整路径名字
- newInstance()
    - 创建类的实例
- getPackage()
    - 获得类的包
- getSimpleName()
    - 获得类的名字
- getSuperclass()
    - 获得当前类继承的父类的名字
- getInterfaces()
    - 获得当前类实现的类或是接口
- getField(String name)
    - 获得某个公有的属性对象
- getFields()
    - 获得所有公有的属性对象
- getDeclaredField(String name)
    - 获得某个属性对象
- getDeclaredFields()
    - 获得所有属性对象
- getAnnotation(Class<A> annotationClass)
    - 返回该类中与参数类型匹配的公有注解对象
- getAnnotations()
    - 返回该类所有的公有注解对象
- getDeclaredAnnotation(Class<A> annotationClass)
    - 返回该类中与参数类型匹配的所有注解对象
- getDeclaredAnnotations()
    - 返回该类所有的注解对象
- getConstructor(Class...<?> parameterTypes)
    - 获得该类中与参数类型匹配的公有构造方法
- getConstructors()
    - 获得该类的所有公有构造方法
- getDeclaredConstructor(Class...<?> parameterTypes)
    - 获得该类中与参数类型匹配的构造方法
- getDeclaredConstructors()
    - 获得该类所有构造方法
- getMethod(String name, Class...<?> parameterTypes)
    - 获得该类某个公有的方法
- getMethods()
    - 获得该类所有公有的方法
- getDeclaredMethod(String name, Class...<?> parameterTypes)
    - 获得该类某个方法
- getDeclaredMethods()
    - 获得该类所有方法
- isAnnotation()
    - 如果是注解类型则返回true
- isAnnotationPresent(Class<? extends Annotation> annotationClass)
    - 如果是指定类型注解类型则返回true
- isAnonymousClass()
    - 如果是匿名类则返回true
- isArray()
    - 如果是一个数组类则返回true
- isEnum()
    - 如果是枚举类则返回true
- isInstance(Object obj)
    - 如果obj是该类的实例则返回true
- isInterface()
    - 如果是接口类则返回true
- isLocalClass()
    - 如果是局部类则返回true
- isMemberClass()
    - 如果是内部类则返回true

Field相关
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- equals(Object obj)
    - 属性与obj相等则返回true
- get(Object obj)
    - 获得obj中对应的属性值
- set(Object obj, Object value)
    - 设置obj中对应属性值

Method相关
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- invoke(Object obj, Object... args)
    - 传递object对象及参数调用该对象对应的方法

Constructor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- newInstance(Object... initargs)
    - 根据传递的参数创建类的对象
