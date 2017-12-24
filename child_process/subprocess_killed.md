<!-- YAML
added: v0.5.10
-->

* {boolean} Set to `true` after `subprocess.kill()` is used to successfully
  send a signal to the child process.

The `subprocess.killed` property indicates whether the child process
successfully received a signal from `subprocess.kill()`. The `killed` property
does not indicate that the child process has been terminated.

<a name="child_process_child_pid"></a>
