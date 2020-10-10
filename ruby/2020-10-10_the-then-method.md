# The then method

I knew about `tap`, but not `then`, the difference is that `tap` returns `self`
whereas `then` returns the return value of the block.

My use case was that I had a flat list of pairs, with one element at the
beginning, and I wanted a list of pairs, like that:

```ruby
# I had
['a', 'k1', 'v1', 'f2', 'k2']
# I wanted
[['k1', 'v1'], ['f2', 'k2']]
```

And I got there thanks to `then`:

```ruby
['a', 'k1', 'v1', 'f2', 'k2'].then do |x|
  x.shift
  x.each_slice(2)
end
```

https://ruby-doc.org/core-2.7.1/Object.html#tap-method
https://ruby-doc.org/core-2.7.1/Object.html#then-method
