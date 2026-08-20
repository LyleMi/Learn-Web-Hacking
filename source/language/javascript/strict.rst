strict mode
========================================

Introduction
----------------------------------------
In ES5, in addition to the normal running mode, strict mode is added, which allows the code to explicitly break out of the "sloppy mode/sloppy mode" and run under more strict conditions. Strict mode is not just a subset: it was created to have different semantics than normal code.

The main purposes of introducing strict mode are:

- Eliminated some original silent errors by throwing errors
- Eliminate some unreasonable and imprecise aspects of JavaScript syntax and reduce some weird behaviors
- Eliminate some unsafe aspects of code operation and ensure the safety of code operation
- Fixed some defects that made it difficult for the JavaScript engine to perform optimization, improved compiler efficiency and increased running speed
- Disabled some syntax that may be defined in future versions of ECMAScript to pave the way for new versions of JavaScript in the future

call
----------------------------------------
Strict mode is enabled using the ``"use strict";`` string. For the entire script file, you can put ``"use strict"`` at the first line of the script file to run the entire script in strict mode. If this line of statement is not in the first line, it will not take effect and will run in normal mode.

For a single function, if ``"use strict"`` is placed on the first line of the function body, the entire function will run in strict mode.

behavior change
----------------------------------------
In strict mode, there are mainly the following behavior changes:

Explicit declaration of global variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In normal mode, if a variable is assigned a value without being declared, it defaults to a global variable. Strict mode prohibits this usage and global variables must be declared explicitly.

.. code-block:: javascript

    "use strict";
    for(i = 0; i < 2; i++) { // ReferenceError: i is not defined
    }

Do not use the with statement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The with statement cannot determine at compile time which object the attribute belongs to. This will affect compilation efficiency, so it is prohibited in strict mode.

Create eval scope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In normal mode, the scope of the eval statement depends on whether it is in the global scope or the function scope. In strict mode, the eval statement itself is a scope and can no longer generate global variables. The variables it generates can only be used inside eval.

Disable deletion of variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Variables cannot be deleted in strict mode. Only object properties with configurable set to true can be deleted.

Explicit error reporting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In normal mode, some errors will only fail silently, but in strict mode, errors will be reported, including the following scenarios:

- Assign a value to a read-only property of an object
- Assign a value to a property read using the getter method
- Add new properties to objects that prohibit extension
- Delete an undeletable attribute

syntax error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Strict mode introduces some new syntax errors, including:

- Objects cannot have attributes with duplicate names.
- Functions cannot have parameters with duplicate names
- disallow octal representation
- Functions must be declared at the top level
- Added reserved words
    - class
    - enum
    - export
    - extends
    - import
    - super

Security enhancement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Prohibit this keyword from pointing to the global object
- Disable call stack traversal inside a function

Limit arguments object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Assignment to arguments is not allowed
- arguments no longer tracks parameter changes
- Use of arguments.callee is prohibited
