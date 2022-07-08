# Use scoping to apply a scope to a block

Say you have a scope in an Active Record model like:

```ruby
scope :published, -> { where(published: true) }
```

And for some reason you want the scope to be applied to all the queries in a
block, you need to use [`scoping`][1]:

```ruby
Model.published.scoping do
  Model.first # will use the scope
end
```

Because doing this is essentially useless:

```ruby
Model.published.scoping do
  Model.first # will use the scope
end
```


[1]:http://api.rubyonrails.org/classes/ActiveRecord/Relation.html#method-i-scoping
