# Forcing integer overflow

As I was thinking about how to implement the
[`BITOP`][https://redis.io/commands/bitop] command for Redis in Ruby Chapter
10, I started to wonder how to implement the wrap-around logic.

For instance if the type is set to u4, 15 + 1 should result in 0, which isn't too hard, we could do something like:

```
current_value + increment & 2**number_of_bits
```

But what about signed integer, with i4, 7 + 1 should result in -8. That's
because 7 (0111) + 1 is 1000, which is the representation of -8 in two's
complement. So I was wondering how to get to that and ...

```
~
```

The not operator!

```
~7 # => -8, expected result for i4
~-8 # => 7


~3 # => -4 expected result for i3
~-4 # => 3
```

Looking at 7 as an example, 7 is 0111, if we flip all the bits we end up with
1000, which is -8, TADA, done!

https://en.wikipedia.org/wiki/Two%27s_complement
