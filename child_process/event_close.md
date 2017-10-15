<!-- YAML
added: v0.7.7
-->

* `code` {number} The exit code if the child exited on its own.
* `signal` {string} The signal by which the child process was terminated.

The `'close'` event is emitted when the stdio streams of a child process have
been closed. This is distinct from the [`'exit'`][] event, since multiple
processes might share the same stdio streams.

