Xpath injection
================================

Xpath definition
--------------------------------
XPath injection attacks take advantage of the loose input and fault-tolerant features of the XPath parser to attach malicious XPath query code to URLs, forms, or other information to gain access to permission information and change this information. XPath injection attack is a new attack method applied to Web services. It allows an attacker to obtain the complete content of an XML document through XPath query without knowing the relevant knowledge of XPath query in advance.

Xpath injection attack principle
--------------------------------
 XPath injection attacks mainly work by constructing special inputs. These inputs are often some combinations in XPath syntax. These inputs will be passed into the Web application as parameters, and the operations desired by the intruder will be performed by executing XPath queries. The following takes the module in login verification as an example to illustrate the implementation principle of XPath injection attacks.

In the login verification program of a Web application, there are generally two parameters: username and password. The program will perform authorization operations through the username and password submitted by the user. If the verification data is stored in an XML file, the principle is to authorize access by looking up the results of the username (username) and password (password) in the user table.

An example exists in the user.xml file as follows:
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

The typical query statement in XPath is: ``//users/user[loginID/text()='xyz'and password/text()='123test']``

However, the following methods can be used to implement injection attacks and bypass authentication. If the user passes in a login and password, such as ``loginID = 'xyz' and password = '123test'``, the query statement will return true. But if the user passes in a value like ``' or 1=1 or ''='``, then the query statement will also get a true return value, because the XPath query statement will eventually become the following code: ``//users/user[loginID/text()=''or 1=1 or ''='' and password/text()='' or 1=1 or ''='']``

This string would logically cause the query to always return true and would always allow the attacker to access the system. An attacker can leverage XPath to dynamically manipulate XML documents within an application. After the attack completes the login, the highest-privilege account and other important document information can be obtained through XPath blind entry technology.
