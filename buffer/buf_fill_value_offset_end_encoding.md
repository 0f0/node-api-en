<!-- YAML
added: v0.5.0
changes:
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4935
    description: The `encoding` parameter is supported now.
-->

* `value` {string|Buffer|integer} The value to fill `buf` with.
* `offset` {integer} Number of bytes to skip before starting to fill `buf`. **Default:** `0`
* `end` {integer} Where to stop filling `buf` (not inclusive). **Default:** [`buf.length`]
* `encoding` {string} If `value` is a string, this is its encoding.
  **Default:** `'utf8'`
* Returns: {Buffer} A reference to `buf`.

Fills `buf` with the specified `value`. If the `offset` and `end` are not given,
the entire `buf` will be filled. This is meant to be a small simplification to
allow the creation and filling of a `Buffer` to be done on a single line.

Example: Fill a `Buffer` with the ASCII character `'h'`

```js
const b = Buffer.allocUnsafe(50).fill('h');

// Prints: hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh
console.log(b.toString());
```

`value` is coerced to a `uint32` value if it is not a String or Integer.

If the final write of a `fill()` operation falls on a multi-byte character,
then only the first bytes of that character that fit into `buf` are written.

Example: Fill a `Buffer` with a two-byte character

```js
// Prints: <Buffer c8 a2 c8>
console.log(Buffer.allocUnsafe(3).fill('\u0222'));
```

