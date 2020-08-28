# Multiplying by power of twos and bit shifts

Based on code I saw
(https://github.com/pjambet/til/blob/master/misc/2020-08-28_a-simple-hash-function.md
for instance), it looks like a shortcut to multiply a number by "power of two + 1" is to use a left bitshift by the power of the previous number and the
number, here's an example because that wasn't clear:

33 is 2**5 + 1, so n * 33 is also (n << 5) + n

It seems to work with all power of twos:

65 is 2**6 + 1, so n * 65 is also (n << 6) + n

Not a proof, but just to test, it seems to work:

``` ruby
random_number = rand 10_000_000_000
(1..1_000).each do |i|
  unless (random_number * (2**(i)+1) == (random_number << i) + random_number )
    raise "Yo, that doesn't work for #{ i }"
  end
end
```
