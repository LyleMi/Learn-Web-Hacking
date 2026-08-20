Asynchronous mechanism
========================================

async / await
----------------------------------------
The async function keyword is used to define an asynchronous function in an expression.

Promise
----------------------------------------
A Promise object is a proxy object (a proxy for a value), and the proxy value may not be known when the Promise object is created. It allows you to bind corresponding handlers for the success and failure of asynchronous operations. This allows an asynchronous method to return a value like a synchronous method, but it does not return the final execution result immediately, but a promise object that represents the result in the future.

A Promise has the following states:

- pending: initial state, neither success nor failure state.
-fulfilled: means the operation was completed successfully.
- rejected: means the operation failed.

A Promise object in the pending state may become fulfilled and pass a value to the corresponding state processing method, or it may become failed (rejected) and pass failure information. When any of these situations occurs, the handlers bound to the Promise object's then method will be called (the then method contains two parameters: onfulfilled and onrejected, both of which are Function types. When the Promise state is fulfilled, then's onfulfilled method is called, and when the Promise state is rejected, then's onrejected method is called, so there is no competition between the completion of the asynchronous operation and the bound handler method).

Because the Promise.prototype.then and Promise.prototype.catch methods return promise objects, they can be chained.

execution queue
----------------------------------------
The asynchronous running mechanism in JavaScript is as follows:
    
- All synchronization tasks are executed on the main thread, forming an execution stack
- In addition to the main thread, there is also a task queue. As long as the asynchronous task has running results, an event is placed in the task queue.
- Once all synchronization tasks in the execution stack have been executed, the system reads the task queue to see what events are in it. Those corresponding asynchronous tasks end the waiting state, enter the execution stack, and start execution.
- The main thread keeps repeating the third step above.

The browser's kernel is multi-threaded. Different asynchronous operations in the browser's kernel are scheduled and executed by different browser kernel modules. Asynchronous operations will add relevant callbacks to the task queue. It can be divided into three types: DOM events, time callbacks, and network callbacks:

- DOM events: processed by the DOM module of the browser kernel. When the event is triggered, the callback function will be added to the task queue.
- Time callback: functions such as setTimeout / setInterval will be delayed by the timer module of the browser kernel. When the time arrives, the callback function will be added to the task queue.
- Network callbacks: ajax / fetch, etc. are handled by the network module of the browser kernel. The callbacks are added to the task queue after the network request is completed and returned.
