other
========================================

Command execution
----------------------------------------
The child_process.exec command in Node.js calls ``/bin/sh``, so you can use this command to execute the shell directly.

Anti-debugging skills
----------------------------------------
- Function redefinition ``console.log = function(a){}``
- Timed breakpoint ``setInterval(function(){debugger}, 1000);``

Object copy
----------------------------------------
Object copies in JavaScript are divided into shallow copies and deep copies.

When copying an object, only the reference of the copy object is copied, but the copy object and the source object still refer to the same entity. Changes to one object will affect another object.

When copying an object in a deep copy, not only does it copy the reference of the object, but also copies the values referenced by the object together. The source object and the copy object are independent of each other, and any changes to any object will not affect the other object.

Deep copy can be implemented based on ``for-in`` / ``object.assign()`` / extension operator ``...`` / ``JSON.parse(JSON.stringify())``` and so on . The first three methods only make deep copy of the first layer. If the object structure is more complex, it is necessary to copy deeper levels in a recursive manner.

Common Sink
----------------------------------------
- child_process
- eval
- exec
- execSync
