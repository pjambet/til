# Build a fixed size array from scratch

Using the Fiddle library, we can use `malloc` and build an array from Scract,
which provides indexed access in O(1)

The biggest hurdle was dealing with the `Fiddle::Pointer` class given its
limited documentation. The following uses the `Marshal` library to deal with
any types, at the cost of what is probably a terrible runtime performance
combined with a wasteful storage system

```ruby
require 'fiddle'

class BYOArray < BasicObject

  PTR_SIZE = ::Fiddle::SIZEOF_LONG

  def initialize(max_size)
    @max_size = max_size
    @current_size = 0
    @beginning_address = ::Fiddle::Pointer.malloc(PTR_SIZE)
  end

  def add(str)
    ::Kernel.raise 'Array is full' if @current_size == @max_size

    ptr = ::Fiddle::Pointer.to_ptr(::Marshal.dump(str))
    offset = @current_size * PTR_SIZE # 0 at first, then 8, 16, etc ...

    @beginning_address[offset, PTR_SIZE] = ptr.ref

    @current_size += 1
    self
  end

  def get(i)
    return nil if i < 0 || i >= @current_size

    address = @beginning_address[i * PTR_SIZE, PTR_SIZE].unpack('Q')[0]
    ::Marshal.load(::Fiddle::Pointer.new(address).to_s)
  end

  def to_s
    "Size: #{ @current_size }"
  end
end
```

See: https://gist.github.com/pjambet/01b54af23790b9a279c45ae07c7ec4a5
