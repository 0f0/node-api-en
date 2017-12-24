<!-- YAML
added: v0.1.16
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9587
    description: Added `external` to the returned object.
-->

* Returns: {Object}
    * `rss` {integer}
    * `heapTotal` {integer}
    * `heapUsed` {integer}
    * `external` {integer}

The `process.memoryUsage()` method returns an object describing the memory usage
of the Node.js process measured in bytes.

For example, the code:

```js
console.log(process.memoryUsage());
```

Will generate:

<!-- eslint-skip -->
```js
{
  rss: 4935680,
  heapTotal: 1826816,
  heapUsed: 650472,
  external: 49879
}
```

`heapTotal` and `heapUsed` refer to V8's memory usage.
`external` refers to the memory usage of C++ objects bound to JavaScript
objects managed by V8. `rss`, Resident Set Size, is the amount of space
occupied in the main memory device (that is a subset of the total allocated
memory) for the process, which includes the _heap_, _code segment_ and _stack_.

The _heap_ is where objects, strings and closures are stored. Variables are
stored in the _stack_ and the actual JavaScript code resides in the
_code segment_.

