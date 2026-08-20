prototype chain
========================================

Explicit prototypes and implicit prototypes
----------------------------------------
JavaScript prototypes are divided into explicit prototypes (explicit prototype property) and implicit prototypes (implicit prototype link).

The explicit prototype refers to prototype, which is an attribute of the function. This attribute is a pointer, pointing to an object, and displays the attribute of modifying the prototype of the object. Only functions have this attribute.

Implicit prototype refers to the built-in property prototype of any object in JavaScript. There was no standard way to access this built-in property prior to ES5, but most browsers support access via __proto__. ES5 has a standard Get method for this built-in property ``Object.getPrototypeOf()``.

The implicit prototype points to the prototype of the function (constructor) that created the object, ``__proto__`` points to the prototype object of the current object, and prototype points to the prototype object of the object constructed with the current function as the constructor.

The role of explicit prototypes is to implement prototype-based inheritance and attribute sharing.
Implicit prototypes are used to form prototype chains and are also used to implement prototype-based inheritance. For example, when we access the x attribute in the object obj, if it is not found in obj, it will be searched along ``__proto__``.

::

  Note: Object.prototype 这个对象是个例外，它的__proto__值为null

new process
----------------------------------------

.. code-block:: javascript

  var Person = function(){};
  var p = new Person();

The new process is divided into the following three steps:
- ``var p={};`` Initialize an object p
- ``p.__proto__ = Person.prototype;``
- ``Person.call(p);`` Construct p, which can also be called initializing p

The key lies in the second step, let's prove it:

.. code-block:: javascript

  var Person = function(){};
  var p = new Person();
  alert(p.__proto__ === Person.prototype);

This code will return true. This shows that our step 2 is correct.

Example
----------------------------------------

.. code-block:: javascript

  var Person = function(){};
  Person.prototype.sayName = function() {
      alert("My Name is Jacky");
  };

  Person.prototype.age = 27;
  var p = new Person();
  p.sayName();

p is an object that references Person. We defined a sayName method and age attribute on the prototype of Person. When we execute p.age, we will first search inside this (that is, inside the constructor). If it is not found, we will trace it back along the prototype chain.

How does the upward tracing here work upward? Here we need to use the ``__proto__`` attribute to link to the prototype (that is, Person.prototype) for search. Finally found the age attribute on the prototype.

Prototype chain pollution
----------------------------------------
As mentioned before, JavaScript is a dynamic inheritance. When modifying its own object through ``__proto__``, it will affect objects with the same prototype. Therefore, when the key-value pair is controllable by the user, prototype chain pollution may occur.
