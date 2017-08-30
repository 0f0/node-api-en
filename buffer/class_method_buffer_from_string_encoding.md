<!-- YAML
added: v5.10.0
-->

* `string` {string} A string to encode.
* `encoding` {string} The encoding of `string`. **Default:** `'utf8'`

Creates a new `Buffer` containing the given JavaScript string `string`. If
provided, the `encoding` parameter identifies the character encoding of `string`.

Examples:

```js
const buf1 = Buffer.from('this is a tést');

// Prints: this is a tést
console.log(buf1.toString());

// Prints: this is a tC)st
console.log(buf1.toString('ascii'));


const buf2 = Buffer.from('7468697320697320612074c3a97374', 'hex');

// Prints: this is a tést
console.log(buf2.toString());
```

A `TypeError` will be thrown if `str` is not a string.

