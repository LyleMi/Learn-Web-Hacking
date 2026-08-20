Scope and closure
========================================

Scope and scope chain
----------------------------------------

Scope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Simply put, scope is the accessible range of variables and functions, that is, scope controls the visibility and life cycle of variables and functions. The scope of JavaScript is formed by functions, which means that the variables of a function cannot be accessed outside the function.

Scope can be divided into global scope, local scope and block-level scope. Among them, global scope mainly has the following three situations:

- Variables defined outside the function have global scope
- Variables that are not defined for direct assignment are automatically declared to have global scope
- The properties of the window object have global effects

Local scope is generally only accessible within a fixed fragment of code, most commonly within a function, so this scope is also called function scope.

scope leak
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the ES5 standard, there are only global scopes and local scopes, and there is no block-level scope, which may cause variable leakage problems. For example:

.. code-block:: javascript

    var i = 1;
    function f() {
        console.log(i)
        if (true) {
            var i = 2;
        }
    }
    f(); // undefined

Scope hoisting (var Hoisting)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In JavaScript, using var to declare a variable anywhere within a function or global is equivalent to declaring it at the top within it. This behavior is called Hoisting. For example, the following code is equivalent to the second code

.. code-block:: javascript

    function foo() {
        console.log(x); // => undefined
        var x = 1;
        console.log(x); // => 1
    }
    foo();

.. code-block:: javascript

    function foo() {
        var x;
        console.log(x); // => undefined
        x = 1;
        console.log(x); // => 1
    }
    foo();

scope chain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When a function is executed, local variables are always searched from inside the function first. If the corresponding variable cannot be found, it will be searched in the superior scope where the function was created until the global scope is found. This process is called a scope chain.

closure
----------------------------------------
A function together with a reference to its state, the lexical environment, forms a closure. That is, closures allow you to access the outer function scope from the inner function. In JavaScript, functions generate closures every time they are created.

In JavaScript, there is no native support for private methods, that is, an element/method can only be called by other methods in the same class. Closures are a scheme that can be used to simulate private methods. In addition, closures also provide the ability to manage the global namespace to prevent non-core methods or attributes from polluting the public interface part of the code. Here's a simple example:

.. code-block:: javascript

    var Counter = (function() {
      var privateCounter = 0;
      function changeBy(val) {
        privateCounter += val;
      }
      return {
        increment: function() {
          changeBy(1);
        },
        decrement: function() {
          changeBy(-1);
        },
        value: function() {
          return privateCounter;
        }
      }   
    })();

    console.log(Counter.value()); /* logs 0 */
    Counter.increment();
    Counter.increment();
    console.log(Counter.value()); /* logs 2 */
    Counter.decrement();
    console.log(Counter.value()); /* logs 1 */

global object
----------------------------------------
A global object is a special object whose scope is global.

The global object available on all platforms is ``globalThis``, which has the same value as this in the global scope. In addition, there are ``self`` and ``window`` global objects in browsers, ``self`` global objects in Web Workers, and ``global`` global objects in Node.js.
