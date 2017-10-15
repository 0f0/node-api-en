<!-- YAML
added: v0.4.2
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v4.1.0
    pr-url: https://github.com/nodejs/node/pull/2387
    description: Numeric strings, `NaN` and `Infinity` are now allowed
                 time specifiers.
-->

* `fd` {integer}
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* `callback` {Function}
  * `err` {Error}

Change the file system timestamps of the object referenced by the supplied file
descriptor. See [`fs.utimes()`][].

*Note*: This function does not work on AIX versions before 7.1, it will return
the error `UV_ENOSYS`.

