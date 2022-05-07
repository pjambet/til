# piping output creates a new process

```ruby
spawn('yes')
```

creates a single process you can kill, but


```ruby
spawn('yes 2> /dev/null')
```

Creates a parent process and a subprocess, so you can't easily kill `yes`
