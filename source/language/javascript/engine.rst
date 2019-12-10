引擎
========================================

V8
----------------------------------------
V8是Chrome的JavaScript语言处理程序（VM）。其引擎由TurboFan、Ignition和Liftoff组成。其中Turbofan是其优化编译器，Ignition则是其解释器，Liftoff是WebAssembly的代码生成器。

SpiderMonkey
----------------------------------------
SpiderMonkey是Mozilla项目的一部分，是一个用 C/C++ 实现的JavaScript脚本引擎。

JavaScriptCore
----------------------------------------
JavaScriptCore的优化执行分为四个部分，LLInt、Baseline、DFG、FTL。LLInt是最开始的解释执行部分，Baseline是暂时的JIT，DFG阶段开始做一定的优化，FTL阶段做了充分的优化。

ChakraCore
----------------------------------------
ChakraCore是一个完整的JavaScript虚拟机，由微软实现，用于Edge浏览器以及IE的后期版本中。

JScript
----------------------------------------
JScript是由微软开发的脚本语言，是微软对ECMAScript规范的实现，用于IE的早期版本中。

JerryScript
----------------------------------------
JerryScript是一个适用于嵌入式设备的小型JavaScript引擎，由三星开发并维护。
