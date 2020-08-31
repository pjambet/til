# Print a number as binary

Use `sprintf`, or its short version, `%` with the `%b` template string:

``` ruby
a = rand 1_000_000_000 # => 966,552,315 when I ran it
'%b' % a # => "111001100111000110101011111011"
```

Use `0<number of zeroes` to pad with 0s:

``` ruby
a = rand 1_000_000_000 # => 16,849,156 when I ran it
'%064b' % a # => "111001100111000110101011111011"
```
