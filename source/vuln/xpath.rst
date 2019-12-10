Xpath注入
================================

Xpath定义
--------------------------------
XPath注入攻击是指利用XPath解析器的松散输入和容错特性，能够在 URL、表单或其它信息上附带恶意的XPath 查询代码，以获得权限信息的访问权并更改这些信息。XPath注入攻击是针对Web服务应用新的攻击方法，它允许攻击者在事先不知道XPath查询相关知识的情况下，通过XPath查询得到一个XML文档的完整内容。

Xpath注入攻击原理
--------------------------------
 XPath注入攻击主要是通过构建特殊的输入，这些输入往往是XPath语法中的一些组合，这些输入将作为参数传入Web 应用程序，通过执行XPath查询而执行入侵者想要的操作，下面以登录验证中的模块为例，说明 XPath注入攻击的实现原理。

在Web 应用程序的登录验证程序中，一般有用户名（username）和密码（password） 两个参数，程序会通过用户所提交输入的用户名和密码来执行授权操作。若验证数据存放在XML文件中，其原理是通过查找user表中的用户名 （username）和密码（password）的结果来进行授权访问，

例存在user.xml文件如下：
::

    <users>
         <user>
             <firstname>Ben</firstname>
             <lastname>Elmore</lastname>
             <loginID>abc</loginID>
             <password>test123</password>
         </user>
         <user>
             <firstname>Shlomy</firstname>
             <lastname>Gantz</lastname>
             <loginID>xyz</loginID>
             <password>123test</password>
         </user>

则在XPath中其典型的查询语句为： ``//users/user[loginID/text()='xyz'and password/text()='123test']``

但是，可以采用如下的方法实施注入攻击，绕过身份验证。如果用 户传入一个 login 和 password，例如 ``loginID = 'xyz' 和 password = '123test'`` ，则该查询语句将返回 true。但如果用户传入类似 ``' or 1=1 or ''='`` 的值，那么该查询语句也会得到 true 返回值，因为 XPath 查询语句最终会变成如下代码：``//users/user[loginID/text()=''or 1=1 or ''='' and password/text()='' or 1=1 or ''='']``

这个字符串会在逻辑上使查询一直返回 true 并将一直允许攻击者访问系统。攻击者可以利用 XPath 在应用程序中动态地操作 XML 文档。攻击完成登录可以再通过XPath盲入技术获取最高权限帐号和其它重要文档信息。
