
<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!--name=vm-->

The `vm` module provides APIs for compiling and running code within V8 Virtual
Machine contexts.

JavaScript code can be compiled and run immediately or
compiled, saved, and run later.

A common use case is to run the code in a sandboxed environment.
The sandboxed code uses a different V8 Context, meaning that
it has a different global object than the rest of the code.

One can provide the context by ["contextifying"][contextified] a sandbox
object. The sandboxed code treats any property on the sandbox like a
global variable. Any changes on global variables caused by the sandboxed
code are reflected in the sandbox object.

```js
const vm = require('vm');

const x = 1;

const sandbox = { x: 2 };
vm.createContext(sandbox); // Contextify the sandbox.

const code = 'x += 40; var y = 17;';
// x and y are global variables in the sandboxed environment.
// Initially, x has the value 2 because that is the value of sandbox.x.
vm.runInContext(code, sandbox);

console.log(sandbox.x); // 42
console.log(sandbox.y); // 17

console.log(x); // 1; y is not defined.
```

*Note*: The vm module is not a security mechanism.
**Do not use it to run untrusted code**.

