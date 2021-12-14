# The difference between preload and includes

preload is one of the two strategies that includes can use. The other is to do
a big join.

I was always confused because in many cases includes does two queries, and
that's what preload does, but with preload it's consistent, with includes you
don't know what you're gonna get

Links:

- https://stackoverflow.com/questions/11946311/whats-the-difference-between-includes-and-preload-in-an-activerecord-query/11947303
- https://api.rubyonrails.org/classes/ActiveRecord/QueryMethods.html#method-i-preload
- https://api.rubyonrails.org/classes/ActiveRecord/QueryMethods.html#method-i-includes
