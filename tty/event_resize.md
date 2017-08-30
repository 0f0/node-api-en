<!-- YAML
added: v0.7.7
-->

The `'resize'` event is emitted whenever either of the `writeStream.columns`
or `writeStream.rows` properties have changed. No arguments are passed to the
listener callback when called.

```js
process.stdout.on('resize', () => {
  console.log('screen size has changed!');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

*Note*: On Windows resize events will be emitted only if stdin is unpaused
(by a call to `resume()` or by adding a data listener) and in raw mode. It can
also be triggered if a terminal control sequence that moves the cursor is
written to the screen. Also, the resize event will only be signaled if the
console screen buffer height was also changed. For example shrinking the
console window height will not cause the resize event to be emitted. Increasing
the console window height will only be registered when the new console window
height is greater than the current console buffer size.

