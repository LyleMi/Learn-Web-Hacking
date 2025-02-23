Xpath injection
================================

Xpath definition
--------------------------------
XPath injection attacks are the ability to attach malicious XPath query code on URLs, forms, or other information to gain access to permission information and change it using the loose input and fault tolerance of the XPath parser. XPath injection attack is a new attack method for web services. It allows attackers to obtain the complete content of an XML document through XPath query without knowing the relevant knowledge of XPath query in advance.

Xpath injection attack principle
--------------------------------
XPath injection attacks mainly involve building special inputs, which are often some combinations of XPath syntax. These inputs will be passed into the web application as parameters, and the intruders want by executing XPath queries. Below is login verification The modules in it are used as an example to illustrate the implementation principle of XPath injection attack.

In the login verification program of a web application, there are generally two parameters: username and password. The program will perform authorization operations through the username and password submitted by the user. If the verification data is stored in an XML file, the principle is to authorize access by looking for the results of the user name (username) and password in the user table.

The user.xml file exists as follows:
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

Then in XPath, its typical query statement is: ``//users/user[loginID/text()='xyz'and password/text()='123test']``

However, the following method can be used to implement the injection attack to bypass authentication. If the user passes in a login and password, such as ``loginID = 'xyz' and password = '123test'``, the query will return true. But if the user passes in a value similar to ``' or 1=1 or ''='``, then the query statement will also get the true return value, because the XPath query statement will eventually become the following code: ``//users /user[loginID/text()=''or 1=1 or ''='' and password/text()='' or 1=1 or ''='']```

This string logically causes the query to return true and will always allow the attacker to access the system. An attacker can use XPath to manipulate XML documents dynamically in an application. After the attack is completed, you can then obtain the highest permission account and other important document information through XPath blind entry technology.
