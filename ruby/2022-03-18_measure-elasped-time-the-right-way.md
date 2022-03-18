# Measure elasped time the right way

Don't use a comparison of two calls to `Time.now` and instead use
`Process.clock_gettime(Process::CLOCK_MONOTONIC)`

From the linked article:

> To recap: system clock is constantly floating and it doesn't move only
> forwards. If your calculation of elapsed time is based on it, you're very
> likely to run into calculation errors or even outages.


Example:

```ruby
starting = Process.clock_gettime(Process::CLOCK_MONOTONIC)
# time consuming operation
ending = Process.clock_gettime(Process::CLOCK_MONOTONIC)
elapsed = ending - starting
elapsed # => 9.183449000120163 seconds
```

Source: https://blog.dnsimple.com/2018/03/elapsed-time-with-ruby-the-right-way/
