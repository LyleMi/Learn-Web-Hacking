Deserialization
========================================

PHP serialization implementation
----------------------------------------

Common Processors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are several types of PHP serialization processing, namely php, php_serialize, php_binary and WDDX (requires support when compiling). The default is php, which can be modified through the ``session.serialize_handler`` in the configuration.

If WDDX support is added during PHP compilation, you can only use WDDX, and WDDX will be deprecated since PHP 7.4. From PHP 5.5.4, php_serialize can be used. php_serialize simply uses the serialize/unserialize function directly internally and does not have the limitations that php and php_binary have.

The format of the PHP processor is: key name + vertical line + value serialized by serialize() function.

The format of the php_binary processor is: the ASCII character corresponding to the length of the key name + the value serialized by the serialize() function.

The format of the php_serialize processor is: an array processed by serialize() function.

Serialization format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The implementation of php_serialize is in ``php-src/ext/standard/var.c``, and the main function is ``php_var_serialize_intern``, and the serialized format is as follows:

- boolean
- ``b:<value>;``
- ``b:1;`` // true
- `` b: 0; `` // false
- integer
- ``i:<value>;``
- double
- ``d:<value>;``
- NULL
- ``N;``
- string
- ``s:<length>:"<value>";``
- ``s:1:"s";``
- array
- ``a:<length>:{key, value};``
- ``a:1:{s:4:"key1";s:6:"value1";}`` // ``array("key1" => "value1");``
- object
- ``O:<class_name_length>:"<class_name>":<number_of_properties>:{<properties>};``
- reference
- Pointer type
- ``R:reference;``
- ``O:1:"A":2:{s:1:"a";i:1;s:1:"b";R:2;}``
- ``$a = new A();$a->a=1;$a->b=&$a->a;``

Private and protected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Private is different from protect variables and public variables and cannot be set directly.

The private attribute can only be accessed within the class it is defined and will not be inherited. The class name is preceded by the attribute, that is, ``%00className%00`` is used to calibrate it is private.

The protected property can be accessed in the parent and child classes, and the variable is added before the ``%00*%00`` to calibrate it is protected.

PHP deserialization vulnerability
----------------------------------------
When deserializing, php will call functions such as ``__wakeup` / ``__sleep``, which may cause problems such as code execution. If there is no related function, the related destructor will also be called during destruction, which will also cause code execution.

In addition, the ``__toString`` / ``__call`` two functions are also possible to use.

where ``__wakeup` is fired during deserialization, ``__destruct` is fired during GC, ``__toString`` is fired during echo, ``__call`` is fired during an undefined function call Triggered.


Here is a simple demo.

.. code:: php

class Demo
{

public $data;

public function __construct($data)
{
$this->data = $data;
echo "construct<br />";
}

public function __wakeup()
{
echo "wake up<br />";
}

public function __destruct()
{
echo "Data's value is $this->data. <br />";
echo "destruct<br />";
}
}

var_dump(serialize(new Demo("raw value")));



Output

::

construct
Data's value is raw value.
destruct
string(44) "O:4:"Demo":1:{s:4:"data";s:9:"raw value";}"

After modifying the serialized string, execute

``unserialize('O:4:"Demo":1:{s:4:"data";s:15:"malicious value";}');``

Output

::

wake up
Data's value is malicious value.
destruct

See here that the value has been modified.

The above is a simple application of ``unserialize()`. It is not difficult to see that if ``__wakeup()` or ``__desturct()` has sensitive operations, such as reading and writing files or operating databases, you can use functions. Implement the behavior of reading and writing files or reading data.

So, can you add judgment to ``__wakeup()`` to prevent this vulnerability?
In ``__wakeup()`` we add a line of code

.. code:: php

public function __wakeup()
{
if($this->data != 'raw value') $this->data = 'raw value';
echo "wake up<br />";
}

But in fact, it can still be bypassed. In versions such as PHP5 < 5.6.25 and PHP7 < 7.0.10, there are loopholes in wakeup. When the number of objects in deserialization is not equal to the previous number, wakeup will be bypassed, so use the following payload

::

unserialize('O:7:"HITCON":1:{s:4:"data";s:15:"malicious value";}');

Output

::

Data's value is malicious value.
destruct

Here wakeup is bypassed, and the value is still modified.

Utilization point
----------------------------------------

SoapClient Native Utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The SoapClient class in php can create soap data packets. In non-wsdl mode, when the instance of SoapClient is deserialized, a soap request will be made to the url specified by the second parameter. This feature can be used in SSRF.

ZipArchive native utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the flag parameter in php native class ``ZipArchive::open()`` is set to ``ZipArchive::OVERWRITE``, the specified file will be deleted. This feature can be used to delete files under certain conditions.

Session
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In PHP, session is stored in file form by default. The file is named after session_sessionid. When the session is controlled to a certain extent, deserialization can be triggered through session.

Related CVE
----------------------------------------

CVE-2016-7124
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before PHP 5.6.25 and before 7.0.10, ``__wakeup()`` will not be executed when the number of attributes (variables) of an object is greater than the actual number.
