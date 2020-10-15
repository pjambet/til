# A simple Hash function

Found on http://www.cse.yorku.ca/~oz/hash.html, here is a ruby implementation
of djb2:

```ruby
def djb2(string)
  hash = 5381
  string.chars.each do |char|
    # Equivalent to: hash * 33 + char.ord
    hash = ((hash << 5) + hash) + char.ord
  end
  hash
end
```

Some info about 5381 and 33:
https://stackoverflow.com/questions/1579721/why-are-5381-and-33-so-important-in-the-djb2-algorithm
