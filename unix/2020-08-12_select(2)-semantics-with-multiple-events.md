# select(2) semantics with multiple events

select(2) works with what looks like a queue of events for the sockets you give
it. What this means in practice is that, say that a socket first receives data
from the other end, and then receives EOF, if you call select after that,
select will return twice.

Example in Ruby:

First start a server:

```ruby
irb(main):001:0> require 'socket'
=> true
irb(main):002:0> server = TCPServer.new "localhost", 2000
irb(main):003:0> client = server.accept
```

In another `irb`, connect from a client:

```ruby
irb(main):002:0> socket = TCPSocket.new 'localhost', 2000
```

The call to `accept` in the first `irb` should have returned

Still in the client, write to the server and then close the connection:

```ruby
irb(main):003:0> socket.write "YO!"
=> 3
irb(main):004:0> socket.close
=> nil
```

Back to the server:

```ruby
irb(main):004:0> IO.select [client]
=> [[#<TCPSocket:fd 12, AF_INET6, ::1, 2000>], [], []]
irb(main):005:0> client.read
=> "YO!"
```

That was the result of the first event, the `write` from the client

We can call `select` one more time and it won't block:

``` ruby
irb(main):006:0> IO.select [client]
=> [[#<TCPSocket:fd 12, AF_INET6, ::1, 2000>], [], []]
irb(main):009:0> client.read_nonblock(1024, exception: false)
=> nil
irb(main):010:0> client.eof?
=> true
```

We reached EOF, so we can now close the socket on the server side since the
other side hung up:

```ruby
client.close
```
