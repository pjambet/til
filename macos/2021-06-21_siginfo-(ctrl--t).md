# SIGINFO (Ctrl -T)

Technically not a macOS-only thing, seems to be BSD specific, but hitting
Ctrl-T in a running process sends SIGINFO, which, if the program handles it
correctly prints information about the running progress.

A common use case is to figure out what's happening when something is handing
and looks stuck.

The default seems to be to print some system stats like:

```
load: 11.43  cmd: ruby 72647 waiting 0.46u 0.21s
```

See: https://www.freebsd.org/cgi/man.cgi?query=siginfo&sektion=3&apropos=0&manpath=FreeBSD+7.1-RELEASE
