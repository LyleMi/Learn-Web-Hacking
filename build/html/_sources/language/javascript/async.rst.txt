Asynchronous mechanism
========================================

async / await
----------------------------------------
The async function keyword is used to define asynchronous functions in expressions.

Promise
----------------------------------------
A Promise object is a proxy object (proxy with a value), and the value being prosecuted may be unknown when the Promise object is created. It allows you to bind the corresponding handling methods (handlers) for the success and failure of asynchronous operations. This allows the asynchronous method to return the value like a synchronous method, but not to return the final execution result immediately, but a promise object that represents future results.

A Promise has the following states:

- pending: The initial state is neither successful nor failed.
- fulfilled: means that the operation is completed successfully.
- rejected: means that the operation failed.

A Promise object with a pending state may become fulfilled and pass a value to the corresponding state processing method, or may become rejected and pass failure information. When either of these cases occurs, the handlers bound by the then method of the Promise object will be called (then method contains two parameters: onfulfilled and onrejected, both of which are Function types. When the Promise state is fulfilled , call then 's onfulfilled method, and when the Promise state is rejected, then 's onrejected method is called, so there is no competition between the completion of asynchronous operation and the binding processing method).

Because the Promise.prototype.then and Promise.prototype.catch methods return promise objects, they can be called chained.

Execution queue
----------------------------------------
The asynchronous operation mechanism in JavaScript is as follows:

- All synchronous tasks are executed on the main thread to form an execution stack
- In addition to the main thread, there is also a task queue. As long as the asynchronous task has a running result, an event is placed in the task queue.
- Once all synchronous tasks in the execution stack are executed, the system will read the task queue to see what events are inside. Those corresponding asynchronous tasks end the waiting state, enter the execution stack, and start execution.
- The main thread keeps repeating the third step above.

The browser's kernel is multi-threaded. In the browser's kernel, different asynchronous operations are scheduled and executed by different browser kernel modules. Asynchronous operations will add related callbacks to the task queue. It can be divided into three types: DOM events, time callbacks, and network callbacks:

- DOM event: handled by the DOM module of the browser kernel. When the event is triggered, the callback function will be added to the task queue.
- Time callback: functions such as setTimeout/setInterval will be delayed by the timer module of the browser kernel. When the time arrives, the callback function will be added to the task queue.
- Network callbacks: ajax/fetch, etc. are processed by the browser kernel's network module. The callbacks are added to the task queue after the network request is completed and returned.
