<!-- YAML
added: v5.10.0
changes:
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/17428
    description: Specifying an invalid string for `fill` now results in a
                 zero-filled buffer.
-->

* `size` {integer} The desired length of the new `Buffer`.
* `fill` {string|Buffer|integer} A value to pre-fill the new `Buffer` with.
  **Default:** `0`
* `encoding` {string} If `fill` is a string, this is its encoding.
  **Default:** `'utf8'`

Allocates a new `Buffer` of `size` bytes. If `fill` is `undefined`, the
`Buffer` will be *zero-filled*.

Example:

```js
const buf = Buffer.alloc(5);

// Prints: <Buffer 00 00 00 00 00>
console.log(buf);
```

Allocates a new `Buffer` of `size` bytes.  If the `size` is larger than
[`buffer.constants.MAX_LENGTH`] or smaller than 0, a [`RangeError`] will be
thrown. A zero-length `Buffer` will be created if `size` is 0.

If `fill` is specified, the allocated `Buffer` will be initialized by calling
[`buf.fill(fill)`][`buf.fill()`].

Example:

```js
const buf = Buffer.alloc(5, 'a');

// Prints: <Buffer 61 61 61 61 61>
console.log(buf);
```

If both `fill` and `encoding` are specified, the allocated `Buffer` will be
initialized by calling [`buf.fill(fill, encoding)`][`buf.fill()`].

Example:

```js
const buf = Buffer.alloc(11, 'aGVsbG8gd29ybGQ=', 'base64');

// Prints: <Buffer 68 65 6c 6c 6f 20 77 6f 72 6c 64>
console.log(buf);
```

Calling [`Buffer.alloc()`] can be significantly slower than the alternative
[`Buffer.allocUnsafe()`] but ensures that the newly created `Buffer` instance
contents will *never contain sensitive data*.

A `TypeError` will be thrown if `size` is not a number.

