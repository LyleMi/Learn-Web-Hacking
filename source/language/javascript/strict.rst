Strict mode
========================================

Introduction
----------------------------------------
In ES5, in addition to the normal running mode, strict mode is added, which makes the code explicitly separate from the "sloppy mode/sloppy mode" (sloppy mode) mode under stricter conditions run. Strict pattern is more than just a subset: it is produced to form semantics that are different from normal code.

The purpose of introducing a strict model is mainly to:

- Eliminate some original silent errors by throwing errors
- Eliminate some unreasonable and imperfect aspects of JavaScript syntax and reduce some weird behaviors
- Eliminate some insecurity in code running and ensure the safety of code running
- Fixed some defects that made it difficult for JavaScript engine to perform optimizations, improve compiler efficiency, and increase running speed
- Disable some syntax that may be defined in future versions of ECMAScript to lay the groundwork for newer versions of JavaScript

Call
----------------------------------------
Strict mode is used to enable the string using the ``"use strict";`` string. For the entire script file, you can place ``"use strict"``` first line of the script file to enable the entire script to run in strict mode. If this line is not on the first line, it will not take effect and will run in normal mode.

For a single function, put "use strict"`` on the first line of the function body, and the entire function runs in strict mode.

Behavior change
----------------------------------------
In strict mode, there are mainly the following behavior changes:

Explicit declaration of global variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In normal mode, if a variable is assigned without a declaration, the default is a global variable. Strict mode prohibits this usage, and global variables must be explicitly declared.

.. code-block:: javascript

"use strict";
for(i = 0; i < 2; i++) { // ReferenceError: i is not defined
}

Use with statements are prohibited
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The with statement cannot be determined at compile time. Which object the attribute belongs to, which will affect the compilation efficiency, so it is prohibited in strict mode.

Create an eval scope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In normal mode, the scope of the eval statement depends on whether it is in the global scope or in the functional scope. In strict mode, the eval statement itself is a scope and can no longer generate global variables. The variables it generates can only be used inside eval.

Disable variable deletion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Variables cannot be deleted in strict mode. Only the object properties whose configurable is set to true can be deleted.

An explicit error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some errors will only fail silently in normal mode, but will report errors in strict mode, including the following scenarios:

- Assign read-only properties of an object
- Assign a property read using the getter method
- Add new properties to objects that prohibit expansion
- Delete an undeleteable property

Syntax error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Strict mode has added some syntax errors, including:

- Objects cannot have attributes with duplicate names
- Functions cannot have parameters with duplicate names
- Octal notation is prohibited
- Function must be declared at the top level
- Added reserved words
- class
- enum
- export
- extends
- import
- super

Security enhancement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Forbid this keyword to point to global objects
- Forbidden to traverse the call stack inside the function

Restrict arguments objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Assigning arguments is not allowed
- arguments no longer track changes in parameters
- Prohibit arguments.callee
