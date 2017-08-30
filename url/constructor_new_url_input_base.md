
* `input` {string} The input URL to parse
* `base` {string|URL} The base URL to resolve against if the `input` is not
  absolute.

Creates a new `URL` object by parsing the `input` relative to the `base`. If
`base` is passed as a string, it will be parsed equivalent to `new URL(base)`.

```js
const { URL } = require('url');
const myURL = new URL('/foo', 'https://example.org/');
// https://example.org/foo
```

A `TypeError` will be thrown if the `input` or `base` are not valid URLs. Note
that an effort will be made to coerce the given values into strings. For
instance:

```js
const { URL } = require('url');
const myURL = new URL({ toString: () => 'https://example.org/' });
// https://example.org/
```

Unicode characters appearing within the hostname of `input` will be
automatically converted to ASCII using the [Punycode][] algorithm.

```js
const { URL } = require('url');
const myURL = new URL('https://你好你好');
// https://xn--6qqa088eba/
```

*Note*: This feature is only available if the `node` executable was compiled
with [ICU][] enabled. If not, the domain names are passed through unchanged.

