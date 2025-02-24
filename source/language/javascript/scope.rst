Scope and closure
========================================

Scope and Scope Chain
----------------------------------------

Scope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Simply put, scope is the accessible range of variables and functions, that is, scope controls the visibility and life cycle of variables and functions. The scope of JavaScript is formed by functions, which means that a function's variables cannot be accessed outside the function.

Scopes can be divided into global scope, local scope and block-level scope. The global scope mainly has the following three situations:

- The variables defined outside the function have a global scope
- Variables with undefined direct assignments are automatically declared as having global scope
- The properties of the window object have a global role

Local scopes are generally only accessible within fixed code snippets. The most common one is, for example, inside functions, so this scope is also called function scope.

Scope leak
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the ES5 standard, there are only global scopes and local scopes, and no block-level scopes, which may cause variable leakage problems. For example:

.. code-block:: javascript

was in = 1;
function f() {
console.log(i)
if (true) {
was in = 2;
}
}
f(); // undefined

Scope enhancement (var Hoisting)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In JavaScript, using var to declare a variable anywhere within a function or globally is equivalent to declaring it on the top of its internals, and this behavior is called Hoisting. For example, the following code is equivalent to the second code

.. code-block:: javascript

function foo() {
console.log(x); // => undefined
was x = 1;
console.log(x); // => 1
}
foo();

.. code-block:: javascript

function foo() {
was x;
console.log(x); // => undefined
x = 1;
console.log(x); // => 1
}
foo();

Scope chain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When a function is executed, the local variables are always searched for in-function. If the corresponding variable cannot be found, it will search for the superior scope of the created function until the global scope is found. This process is called the scope chain .

Closure
----------------------------------------
Functions and references to their state, lexical environment, form closures. That is, closures allow you to access external function scopes from internal functions. In JavaScript, functions generate closures each time they are created.

In JavaScript, there is no native support for private methods, that is, an element/method can only be called by other methods in the same class. Closures are a solution that can be used to simulate private methods. In addition, closures also provide the ability to manage global namespaces to avoid non-core methods or attributes pollute the public interface part of the code. Here is a simple example:

.. code-block:: javascript

var Counter = (function() {
was private counter = 0;
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

Global Object
----------------------------------------
A global object is a special object whose scope is global.

The global object available on the entire platform is ``globalThis``, which is the same as this value in the global scope. In addition, there are ``self`` and ``window`` global objects in the browser, ``self`` global objects in Web Workers, and ``global`` global objects in Node.js.
