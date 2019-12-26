作用域与闭包
========================================

作用域与作用域链
----------------------------------------

作用域
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
简单来说，作用域就是变量与函数的可访问范围，即作用域控制着变量与函数的可见性和生命周期。JavaScript的作用域是靠函数来形成的，也就是说一个函数的变量在函数外不可以访问。

作用域可以分为全局作用域、局部作用域和块级作用域，其中全局作用域主要有以下三种情况：

- 函数外面定义的变量拥有全局作用域
- 未定义直接赋值的变量自动声明为拥有全局作用域
- window对象的属性拥有全局作用

局部作用域一般只在固定的代码片段内可访问到，最常见的例如函数内部，所以也会把这种作用域称为函数作用域。

作用域泄漏
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在ES5标准时，只有全局作用域和局部作用域，没有块级作用域，这样可能会造成变量泄漏的问题。例如：

.. code-block:: javascript

    var i = 1;
    function f() {
        console.log(i)
        if (true) {
            var i = 2;
        }
    }
    f(); // undefined

作用域提升（var Hoisting）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在JavaScript中，使用var在函数或全局内任何地方声明变量相当于在其内部最顶上声明它，这种行为称为Hoisting。例如下面这段代码等效于第二段代码

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

作用域链
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
当函数被执行时，总是先从函数内部找寻局部变量，如果找不到相应的变量，则会向创建函数的上级作用域寻找，直到找到全局作用域为止，这个过程被称为作用域链。

闭包
----------------------------------------
函数与对其状态即词法环境（lexical environment）的引用共同构成闭包（closure）。也就是说，闭包可以让你从内部函数访问外部函数作用域。在JavaScript，函数在每次创建时生成闭包。

在JavaScript中，并没有原生的对private方法的支持，即一个元素/方法只能被同一个类中的其它方法所调用。而闭包则是一种可以被用于模拟私有方法的方案。另外闭包也提供了管理全局命名空间的能力，避免非核心的方法或属性污染了代码的公共接口部分。下面是一个简单的例子：

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

全局对象
----------------------------------------
全局对象是一个特殊的对象，它的作用域是全局的。

全平台可用的全局对象是 ``globalThis`` ，它跟全局作用域里的this值相同。另外在浏览器中存在 ``self`` 和 ``window`` 全局对象，Web Workers中存在 ``self`` 全局对象，Node.js 中存在 ``global`` 全局对象。
