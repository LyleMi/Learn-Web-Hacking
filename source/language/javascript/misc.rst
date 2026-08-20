other
========================================

command execution
----------------------------------------
The child_process.exec command in Node.js calls ``/bin/sh``, so you can directly use this command to execute the shell

Anti-debugging techniques
----------------------------------------
- Function redefinition ``console.log = function(a){}``
- Scheduled breakpoint ``setInterval(function(){debugger}, 1000);``

object copy
----------------------------------------
Object copy in JavaScript is divided into shallow copy and deep copy.

When shallow copy copies an object, only the reference of the object is copied, but the copied object and the source object still refer to the same entity. Changes to one object will affect the other object.

When a deep copy copies an object, it not only copies the reference to the object, but also copies the value referenced by the object. The source object and the copy object are independent of each other, and changes to any one object will not affect the other object.

Deep copy can be implemented based on ``for-in`` / ``object.assign()`` / expansion operator ``...`` / ``JSON.parse(JSON.stringify())`` and other methods. The first three methods only make deep copies of the first layer. If the object structure is more complex, you need to use recursion to copy deeper layers.

Common sinks
----------------------------------------
- child_process
- eval
- exec
- execSync
