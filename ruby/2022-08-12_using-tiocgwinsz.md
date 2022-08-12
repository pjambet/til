# Using TIOCGWINSZ

I wanted to replicate the following from [kilo][1] in Ruby:

```c
if (ioctl(1, TIOCGWINSZ, &ws) == -1 || ws.ws_col == 0)
```

I found the followin python ([source][2]):

```python
import sys, struct, fcntl, termios

s = struct.pack('HHHH', 0, 0, 0, 0)
t = fcntl.ioctl(sys.stdout.fileno(), termios.TIOCGWINSZ, s)
print(struct.unpack('HHHH', t))
```

But in Ruby there doesn't seem to be a default lib for termios, so we need the
termios gem:

```
gem install termios
```

`1` in the first example is for STDOUT as we can see in the python example, and
`H` in the Python pack call is for "unsigned short" ([source][3](, as opposed to
`H` in Ruby's pack which is for "hex string (high nibble first)" ([source][4]).
unsigned short in ruby is `S_`. So here we are:

```ruby
irb(main):001:0> require 'termios'
=> true
irb(main):002:0> s = [0, 0, 0, 0].pack("S_S_S_S_")
=> "\x00\x00\x00\x00\x00\x00\x00\x00"
irb(main):003:0> STDOUT.ioctl(Termios::TIOCGWINSZ, s)
=> 0
irb(main):004:0> s.unpack("S_S_S_S_")
=> [67, 116, 1624, 2010]
irb(main):005:0>
```

TADA! 🎉

[1]:https://github.com/antirez/kilo
[2]:https://stackoverflow.com/q/16237137/919641
[3]:https://docs.python.org/3.10/library/struct.html#format-characters
[4]:https://ruby-doc.org/core-3.1.2/Array.html#pack-method
