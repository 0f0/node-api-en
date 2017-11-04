<!-- YAML
added: v0.3.0
changes:
  - version: v8.9.0
    pr-url: https://github.com/nodejs/node/pull/16397
    description: The `paths` option is now supported.
-->

* `request` {string} The module path to resolve.
* `options` {Object}
  * `paths` {Array} Paths to resolve module location from. If present, these
    paths are used instead of the default resolution paths. Note that each of
    these paths is used as a starting point for the module resolution algorithm,
    meaning that the `node_modules` hierarchy is checked from this location.
* Returns: {string}

Use the internal `require()` machinery to look up the location of a module,
but rather than loading the module, just return the resolved filename.

