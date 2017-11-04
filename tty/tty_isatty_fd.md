<!-- YAML
added: v0.5.8
-->

* `fd` {number} A numeric file descriptor

The `tty.isatty()` method returns `true` if the given `fd` is associated with
a TTY and `false` if it is not, including whenever `fd` is not a non-negative
integer.
