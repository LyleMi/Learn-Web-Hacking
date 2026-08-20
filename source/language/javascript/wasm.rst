WebAssembly
========================================

Introduction
----------------------------------------
Simply put, WASM is a new way of distributing code to be executed in the browser. It is a binary language, but cannot run directly on the processor. At runtime, the code is compiled into intermediate byte code that can be quickly converted to machine code within the browser and then executed more efficiently than traditional JavaScript.

implement
----------------------------------------
While browsers may implement Wasm support in different ways, the sandbox environment used is usually the JavaScript sandbox.

When running in a browser, a Wasm application needs to define its code as a separate file or a byte array within a JavaScript block. The file or block of code is then instantiated using JavaScript. Currently it is not possible to call Wasm directly in the page without a JavaScript wrapper.

While Wasm can be written in languages ​​such as C/C++, it itself cannot interact with environments outside of the sandbox. This means that when a Wasm application wants to do something like outputting text, it needs to call a function provided by the browser and then use the browser to output the text somewhere.

Memory in Wasm is linear, it is shared between the Wasm application and JavaScript. When a Wasm function returns a string to JavaScript, it actually returns a pointer to a location within the Wasm application's memory space. The Wasm application itself can only access the portion of JavaScript memory allocated to it, not the entire memory space.

Safety
----------------------------------------
The design of Wasm considers the following aspects to ensure the security of Wasm

- Protect users from applications that cause vulnerabilities due to unintentional errors
- Protect users from applications intentionally written to be malicious
- Provide good mitigations for developers

Specific safety measures include

- Wasm applications run inside a sandbox
- Wasm cannot make function calls to arbitrary addresses. Wasm uses a method of numbering functions, and the numbers are stored in the function table.
- Indirect function calls are subject to type signature checking
- The call stack is protected, which means the return pointer cannot be overwritten
- Implemented control flow integrity, meaning calls to unexpected functions will fail
