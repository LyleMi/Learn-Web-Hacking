engine
========================================

V8
----------------------------------------
V8 is a JavaScript language handler (VM) for Chrome. Its engine consists of TurboFan, Ignition and Liftoff. Among them, Turbofan is its optimization compiler, Ignition is its interpreter, and Liftoff is WebAssembly's code generator.

SpiderMonkey
----------------------------------------
SpiderMonkey is part of the Mozilla project and is a JavaScript scripting engine implemented in C/C++.

JavaScriptCore
----------------------------------------
The optimization execution of JavaScriptCore is divided into four parts: LLInt, Baseline, DFG, and FTL. LLInt is the initial interpretation execution part, Baseline is the temporary JIT, and certain optimizations are started in the DFG stage, and sufficient optimizations are made in the FTL stage.

ChakraCore
----------------------------------------
ChakraCore is a complete JavaScript virtual machine implemented by Microsoft and used in Edge browser as well as in later versions of IE.

JScript
----------------------------------------
JScript is a scripting language developed by Microsoft and is an implementation of the ECMAScript specification by Microsoft and is used in early versions of IE.

JerryScript
----------------------------------------
JerryScript is a small JavaScript engine for embedded devices developed and maintained by Samsung.
