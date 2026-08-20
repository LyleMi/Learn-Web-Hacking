Deserialization
========================================

PHP serialization implementation
----------------------------------------

Common processors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are several types of PHP serialization processing, namely php, php_serialize, php_binary and WDDX (support needs to be enabled during compilation). The default is php, which can be modified through ``session.serialize_handler`` in the configuration.

If PHP is compiled with WDDX support, you can only use WDDX. WDDX has been deprecated since PHP 7.4. php_serialize is available starting with PHP 5.5.4. php_serialize internally simply uses the serialize/unserialize functions directly and does not have the limitations that php and php_binary have.

The format of the PHP processor is: key name + vertical bar + value serialized by the serialize() function.

The format of the php_binary processor is: ASCII characters corresponding to the length of the key name + key name + value serialized by the serialize() function.

The format of the php_serialize processor is: an array serialized by the serialize() function.

serialization format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The implementation of php_serialize is in ``php-src/ext/standard/var.c``. The main function is ``php_var_serialize_intern``. The serialized format is as follows:

- boolean
    - ``b:<value>;``
    - ``b:1;`` // true
    - ``b:0;`` // false
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
    - pointer type
    - ``R:reference;``
    - ``O:1:"A":2:{s:1:"a";i:1;s:1:"b";R:2;}``
    - ``$a = new A();$a->a=1;$a->b=&$a->a;``

private and protect
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unlike protect variables and public variables, private variables cannot be set directly.

The private attribute can only be accessed within the class in which it is defined and will not be inherited. Add the class name before the attribute, that is, ``%00className%00`` to mark it as private.

The protected attribute can be accessed in parent and subclasses. Add ``%00*%00`` before the variable to indicate that it is protected.

PHP Deserialization Vulnerability
----------------------------------------
PHP will call functions such as ``__wakeup`` / ``__sleep`` during deserialization, which may cause problems such as code execution. If there is no related function, the related destructor will also be called during destruction, which will also cause code execution.

In addition, the two functions ``__toString`` / ``__call`` are also possible to use.

Among them, ``__wakeup`` is triggered during deserialization, ``__destruct`` is triggered during GC, ``__toString`` is triggered during echo, and ``__call`` is triggered when an undefined function is called.


A simple demo is provided below.

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



output

::

    construct
    Data's value is raw value.
    destruct
    string(44) "O:4:"Demo":1:{s:4:"data";s:9:"raw value";}" 

After modifying the serialized string, execute

``unserialize('O:4:"Demo":1:{s:4:"data";s:15:"malicious value";}');``

output

::

    wake up
    Data's value is malicious value.
    destruct

As you can see here, the value has been modified.

The above is a simple application of ``unserialize()``. It is not difficult to see that if ``__wakeup()`` or ``__desturct()`` has sensitive operations, such as reading and writing files or operating databases, the behavior of file reading and writing or data reading can be realized through functions.

So, can adding judgment in ``__wakeup()`` prevent this vulnerability?
In ``__wakeup()`` we add a line of code

.. code:: php

    public function __wakeup()
    {
        if($this->data != 'raw value') $this->data = 'raw value';
        echo "wake up<br />";
    }

But it can still be bypassed. Wakeup vulnerabilities exist in versions of PHP5 < 5.6.25 and PHP7 < 7.0.10. When the number of objects in deserialization is different from the previous number, wakeup will be bypassed, so the following payload is used

::

    unserialize('O:7:"HITCON":1:{s:4:"data";s:15:"malicious value";}');

output

::

    Data's value is malicious value.
    destruct

Here wakeup is bypassed and the value is still modified.

Utilization point
----------------------------------------

SoapClient native utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The SoapClient class in PHP can create soap data messages. In non-wsdl mode, when the SoapClient instance is deserialized, it will make a soap request for the URL specified by the second parameter. This feature can be used for SSRF.

ZipArchive native utilization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the flag parameter in the PHP native class ``ZipArchive::open()`` is set to ``ZipArchive::OVERWRITE``, the specified file will be deleted. This feature can be used to delete files under certain conditions.

Session
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In PHP, sessions are stored in the form of files by default. The files are named after sess_sessionid. When the session is controllable to a certain extent, deserialization can be triggered through the session.

Related CVEs
----------------------------------------

CVE-2016-7124
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In versions before PHP 5.6.25 and versions before 7.0.10, when the number of attributes (variables) of an object is greater than the actual number, __wakeup()`` will not be executed.
