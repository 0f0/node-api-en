<!-- YAML
added: v0.11.15
-->

* `value` {integer} Number to be written to `buf`
* `offset` {integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - byteLength`
* `byteLength` {integer} How many bytes to write. Must satisfy: `0 < byteLength <= 6`
* `noAssert` {boolean} Skip `value`, `offset`, and `byteLength` validation?
  **Default:** `false`
* Returns: {integer} `offset` plus the number of bytes written

Writes `byteLength` bytes of `value` to `buf` at the specified `offset`.
Supports up to 48 bits of accuracy. Behavior is undefined when `value` is
anything other than a signed integer.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.allocUnsafe(6);

buf.writeUIntBE(0x1234567890ab, 0, 6);

// Prints: <Buffer 12 34 56 78 90 ab>
console.log(buf);

buf.writeUIntLE(0x1234567890ab, 0, 6);

// Prints: <Buffer ab 90 78 56 34 12>
console.log(buf);
```

