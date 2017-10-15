<!-- YAML
added: v0.5.5
-->

* `offset` {integer} Number of bytes to skip before starting to read. Must satisfy: `0 <= offset <= buf.length - 4`.
* `noAssert` {boolean} Skip `offset` validation? **Default:** `false`
* Returns: {integer}

Reads an unsigned 32-bit integer from `buf` at the specified `offset` with
specified endian format (`readUInt32BE()` returns big endian,
`readUInt32LE()` returns little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([0x12, 0x34, 0x56, 0x78]);

// Prints: 12345678
console.log(buf.readUInt32BE(0).toString(16));

// Prints: 78563412
console.log(buf.readUInt32LE(0).toString(16));

// Throws an exception: RangeError: Index out of range
console.log(buf.readUInt32LE(1).toString(16));
```

