# Less Environment Variables

`less` can take its arguments from the environment variable `LESS`.

For instance, `LESS=N less README.md` is the equivalent to `less -N
README.md` if you want to output line numbers.

Useful to set default config values in a startup script or when
spawmin a new process with its own env, as done in Section 12.3.3 of
Building Git.
