原型链
========================================

显式原型和隐式原型
----------------------------------------
JavaScript的原型分为显式原型（explicit prototype property）和隐式原型（implicit prototype link）。

其中显式原型指prototype，是函数的一个属性，这个属性是一个指针，指向一个对象，显示修改对象的原型的属性，只有函数才有该属性

隐式原型指JavaScript中任意对象都有的内置属性prototype。在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过 ``__proto__`` 来访问。ES5中有了对于这个内置属性标准的Get方法 ``Object.getPrototypeOf()`` 。

隐式原型指向创建这个对象的函数(constructor)的prototype， ``__proto__`` 指向的是当前对象的原型对象，而prototype指向的，是以当前函数作为构造函数构造出来的对象的原型对象。

显式原型的作用用来实现基于原型的继承与属性的共享。
隐式原型的用于构成原型链，同样用于实现基于原型的继承。举个例子，当我们访问obj这个对象中的x属性时，如果在obj中找不到，那么就会沿着 ``__proto__`` 依次查找。

::

  Note: Object.prototype 这个对象是个例外，它的__proto__值为null

new 的过程
----------------------------------------

.. code-block:: javascript

  var Person = function(){};
  var p = new Person();

new的过程拆分成以下三步：
- ``var p={};`` 初始化一个对象p
- ``p.__proto__ = Person.prototype;``
- ``Person.call(p);`` 构造p，也可以称之为初始化p

关键在于第二步，我们来证明一下：

.. code-block:: javascript

  var Person = function(){};
  var p = new Person();
  alert(p.__proto__ === Person.prototype);

这段代码会返回true。说明我们步骤2是正确的。

示例
----------------------------------------

.. code-block:: javascript

  var Person = function(){};
  Person.prototype.sayName = function() {
      alert("My Name is Jacky");
  };

  Person.prototype.age = 27;
  var p = new Person();
  p.sayName();

p是一个引用指向Person的对象。我们在Person的原型上定义了一个sayName方法和age属性，当我们执行p.age时，会先在this的内部查找（也就是构造函数内部），如果没有找到然后再沿着原型链向上追溯。

这里的向上追溯是怎么向上的呢？这里就要使用 ``__proto__`` 属性来链接到原型（也就是Person.prototype）进行查找。最终在原型上找到了age属性。

原型链污染
----------------------------------------
如前文提到的，JavaScript是动态继承，通过 ``__proto__`` 修改自身对象时会影响到有相同原型的对象。因此当键值对是用户可控的情况下，就可能出现原型链污染。
