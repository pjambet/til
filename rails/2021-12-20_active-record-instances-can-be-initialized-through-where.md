# Active Record instances can be initialized through where

You can use `where` to set the values of attributes when calling `new`, or `create`:

```ruby
Post.where(id: 123, title: "Something").new
# => <Post:0x0000 id: 123, title: "Something">
```
