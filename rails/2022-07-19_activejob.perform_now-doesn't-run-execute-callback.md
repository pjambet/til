# ActiveJob.perform_now doesn't run execute callback

Calling Job.perform_now runs "regular" callbacks for `perform` & `enqueue`,
because of [this line][1] but doesn't run the `execute` callbacks, because it's
only run [for `.execute`][2], which is called by the various adapters, like
[for Sidekiq][3]

The `CurrentAttributes` callbacks are [registered here][4] and the callback
around `execute` for Active Job is [registered here][5]

[1]:https://github.com/pjambet/rails/blob/1a22ebc7c1cc824f03ed33e827a1aedee29c7a2e/activejob/lib/active_job/execution.rb#L56-L61
[2]:https://github.com/pjambet/rails/blob/1a22ebc7c1cc824f03ed33e827a1aedee29c7a2e/activesupport/lib/active_support/railtie.rb#L47-L48
[3]:https://github.com/pjambet/rails/blob/1a22ebc7c1cc824f03ed33e827a1aedee29c7a2e/activejob/lib/active_job/queue_adapters/sidekiq_adapter.rb#L41-L43
[4]:https://github.com/pjambet/rails/blob/1a22ebc7c1cc824f03ed33e827a1aedee29c7a2e/activesupport/lib/active_support/railtie.rb#L47-L48
[5]:https://github.com/pjambet/rails/blob/1a22ebc7c1cc824f03ed33e827a1aedee29c7a2e/activejob/lib/active_job/railtie.rb#L50-L58
