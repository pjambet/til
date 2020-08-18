# Shortcut for modulo of a power of two

I was reading the Redis source code, specifically the siphash.c file, as well
as [this Ruby
version][https://github.com/emboss/siphash-ruby/blob/master/lib/siphash.rb#L25]
and I noticed that they both seemed to do achieve the same thing but
differently. Redis used `n & 7` while the Ruby version used `n % 8`

And it turns out that when you're trying to get the power of two modulo of a
number, you can instead do `n & (m-1)` where m is the power of two.

So it works with 2, 4, 8, 16, 32, 64, ... you get it

More info on StackOverflow: https://stackoverflow.com/questions/6670715/mod-of-power-2-on-bitwise-operators
