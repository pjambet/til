# The difference between preload and includes

preload is one of the two strategies that includes can use. The other is to do
a big join.

I was always confused because in many cases includes does two queries, and
that's what preload does, but with preload it's consistent, with includes you
don't know what you're gonna get
