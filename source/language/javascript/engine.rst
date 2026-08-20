engine
========================================

V8
----------------------------------------
V8 is Chrome's JavaScript language processor (VM). Its engine consists of TurboFan, Ignition and Liftoff. Among them, Turbofan is its optimizing compiler, Ignition is its interpreter, and Liftoff is the code generator for WebAssembly.

SpiderMonkey
----------------------------------------
SpiderMonkey is part of the Mozilla project and is a JavaScript script engine implemented in C/C++.

JavaScriptCore
----------------------------------------
The optimization execution of JavaScriptCore is divided into four parts, LLLint, Baseline, DFG, and FTL. LLInt is the initial interpretation and execution part, Baseline is a temporary JIT, certain optimizations are started in the DFG stage, and full optimization is done in the FTL stage.

ChakraCore
----------------------------------------
ChakraCore is a complete JavaScript virtual machine, implemented by Microsoft and used in the Edge browser and later versions of IE.

JScript
----------------------------------------
JScript is a scripting language developed by Microsoft. It is Microsoft's implementation of the ECMAScript specification and was used in early versions of IE.

JerryScript
----------------------------------------
JerryScript is a small JavaScript engine suitable for embedded devices, developed and maintained by Samsung.
