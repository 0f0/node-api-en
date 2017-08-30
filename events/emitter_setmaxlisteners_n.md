<!-- YAML
added: v0.3.5
-->
- `n` {integer}

By default EventEmitters will print a warning if more than `10` listeners are
added for a particular event. This is a useful default that helps finding
memory leaks. Obviously, not all events should be limited to just 10 listeners.
The `emitter.setMaxListeners()` method allows the limit to be modified for this
specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`)
to indicate an unlimited number of listeners.

Returns a reference to the `EventEmitter`, so that calls can be chained.

[`--trace-warnings`]: cli.html#cli_trace_warnings
[`EventEmitter.defaultMaxListeners`]: #events_eventemitter_defaultmaxlisteners
[`domain`]: domain.html
[`emitter.listenerCount()`]: #events_emitter_listenercount_eventname
[`emitter.setMaxListeners(n)`]: #events_emitter_setmaxlisteners_n
[`fs.ReadStream`]: fs.html#fs_class_fs_readstream
[`net.Server`]: net.html#net_class_net_server
[`process.on('warning')`]: process.html#process_event_warning
[`process` object's `uncaughtException` event]: process.html#process_event_uncaughtexception
[stream]: stream.html
