Prototype chain
========================================

Explicit and implicit prototypes
----------------------------------------
JavaScript prototypes are divided into explicit prototype property and implicit prototype link.

The explicit prototype refers to prototype, which is an attribute of the function. This attribute is a pointer, pointing to an object, displaying the properties of the prototype of the modified object. Only the function has this attribute.

Implicit prototype refers to the built-in property prototype that any object in JavaScript has. Before ES5 there was no standard way to access this built-in property, but most browsers support access through ``__proto__`. ES5 has a standard Get method for this built-in attribute ``Object.getPrototypeOf()``.

The implicit prototype points to the prototype of the function (constructor) that creates this object. ``__proto__`` points to the prototype object of the current object, and prototype points to the prototype object of the object constructed with the current function as the constructor.

The function of explicit prototypes is used to realize prototype-based inheritance and sharing of attributes.
Implicit prototypes are used to form prototype chains, and are also used to implement prototype-based inheritance. For example, when we access the x attribute in the object obj, if we cannot find it in obj, we will search in sequence along ``__proto__`.

::

Note: Object.prototype This object is an exception, its __proto__ value is null

The process of new
----------------------------------------

.. code-block:: javascript

var Person = function(){};
was p = new person ();

The new process is divided into the following three steps:
- ``var p={};`` Initialize an object p
- ``p.__proto__ = Person.prototype;``
- ``Person.call(p);`` Construct p, which can also be called initialization p

The key is the second step, let’s prove it:

.. code-block:: javascript

var Person = function(){};
was p = new person ();
alert(p.__proto__ === Person.prototype);

This code will return true. Instructions that our step 2 is correct.

Example
----------------------------------------

.. code-block:: javascript

var Person = function(){};
Person.prototype.sayName = function() {
alert("My Name is Jacky");
};

Person.prototype.age = 27;
was p = new person ();
p.sayName();

p is an object that refers to Person. We define a sayName method and age property on the Person prototype. When we execute p.age, we will first look up inside this (that is, inside the constructor), and if it is not found, then trace up along the prototype chain.

How does the upward traceability go upward here? Here you need to use the ``__proto__`` attribute to link to the prototype (that is, Person.prototype) for searching. Finally, the age attribute was found on the prototype.

Prototype chain pollution
----------------------------------------
As mentioned above, JavaScript is dynamic inheritance. When modifying its own object through ``__proto__`, it will affect objects with the same prototype. Therefore, when the key-value pair is user-controlled, prototype chain pollution may occur.
