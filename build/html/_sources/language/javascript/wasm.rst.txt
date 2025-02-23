WebAssembly
========================================

Introduction
----------------------------------------
In short, WASM is a new way to distribute code to be executed in the browser. It is a binary language, but it cannot run directly on the processor. At runtime, the code is compiled into intermediate byte code, which can be quickly converted into machine code within the browser and then executed more efficiently than traditional JavaScript.

implement
----------------------------------------
While browsers may implement Wasm support in different ways, the sandbox environment used is usually a JavaScript sandbox.

When running in a browser, the Wasm application needs to define its code as a separate file or an array of bytes within a JavaScript block. Then use JavaScript to instantiate files or code blocks. At present, Wasm cannot be called directly in the page without a JavaScript wrapper.

Although Wasm can be written in languages such as C/C++, it itself cannot interact with environments outside the sandbox. This means that when a Wasm application wants to do things like output text, it needs to call the functionality provided by the browser and then use the browser to output the text somewhere.

The memory in Wasm is linear and it is shared between a Wasm application and JavaScript. When the Wasm function returns a string to JavaScript, it actually returns a pointer to a location in the memory space of the Wasm application. The Wasm application itself can only access the portion of the JavaScript memory allocated to it, not the entire memory space.

Safety
----------------------------------------
The design of Wasm is considered from the following aspects to ensure the safety of Wasm

- Protect users from vulnerabilities due to unintentional errors
- Protect users from intentionally written as malicious applications
- Provide good mitigation for developers

Specific safety measures include

- Wasm application runs in a sandbox
- Wasm cannot make function calls to any address. Wasm uses the method of numbering functions, and the numbers are stored in the function table.
- Indirect function calls are subject to type signature checking
- The call stack is protected, which means that the return pointer cannot be overwritten
- Control flow integrity is implemented, which means that unexpected function calls will fail
