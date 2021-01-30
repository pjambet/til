# The path_helper utility initializes the path variable

It apparently reads stuff from `/etc/paths.d/` (and also for man stuff, but I
don't really care about that today, mostly things I want to execute)

The current value returned by `/usr/libexec/path_helper -s` is:

```
PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/TeX/texbin:/usr/local/MacGPG2/bin:/Library/Apple/usr/bin:/Users/pierre/.gem/ruby/3.0.0/bin:/Users/pierre/.rubies/ruby-3.0.0/lib/ruby/gems/3.0.0/bin:/Users/pierre/.rubies/ruby-3.0.0/bin:/opt/homebrew/bin:/Users/pierre/.sdkman/candidates/scala/current/bin:/Users/pierre/.sdkman/candidates/sbt/current/bin:/Users/pierre/.sdkman/candidates/leiningen/current/bin:/Users/pierre/.sdkman/candidates/kotlin/current/bin:/usr/local/sbin:/Users/pierre/.cargo/bin"; export PATH;
```

Clearly there's some custom stuff in there (rubies, sdkman), not sure how these
were able to install stuff somewhere to have them detected by `path_helper`.

The content of my `/etc/paths.d` is:

```
$ ll /etc/paths.d/
total 24
-rwxr-xr-x  1 root  wheel    23B Dec 11 20:01 100-rvictl
-rw-r--r--  1 root  wheel    23B Jan 24  2020 MacGPG2
-rw-r--r--  1 root  wheel    22B Jan 19 17:46 TeX
```

and `/etc/paths`:

```
$ less /etc/paths
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```

I found out about this because I wanted to prepend my arm64 brew directory
(`/opt/homebrew/bin`) to my path, but doing so in `~/.zshenv` was ignored.
Turned out that it's because it was running before `/etc/zprofile`, which runs
`path_helper` and was overriding my stuff: 

See: 

- https://github.com/sorin-ionescu/prezto/tree/master/runcoms
- https://github.com/pjambet/prezto/commit/6d061068ca70466bf1987b60ecd7fdcc02b3b005

What did you learn about unix today
