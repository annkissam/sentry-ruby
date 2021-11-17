<p align="center">
  <a href="https://sentry.io" target="_blank" align="center">
    <img src="https://sentry-brand.storage.googleapis.com/sentry-logo-black.png" width="280">
  </a>
  <br />
</p>

_Bad software is everywhere, and we're tired of it. Sentry is on a mission to help developers write better software faster, so we can get back to enjoying technology. If you want to join us [<kbd>**Check out our open positions**</kbd>](https://sentry.io/careers/)_

Sentry SDK for Ruby
===========

| current version | build | coverage | downloads |
| --- | ----- | -------- | --------- |
| [![Gem Version](https://img.shields.io/gem/v/sentry-ruby?label=sentry-ruby)](https://rubygems.org/gems/sentry-ruby) | [![Build Status](https://github.com/getsentry/sentry-ruby/workflows/sentry-ruby%20Test/badge.svg)](https://github.com/getsentry/sentry-ruby/actions/workflows/sentry_ruby_test.yml) | [![Coverage Status](https://img.shields.io/codecov/c/github/getsentry/sentry-ruby/master?logo=codecov)](https://codecov.io/gh/getsentry/sentry-ruby/branch/master) | [![Downloads](https://img.shields.io/gem/dt/sentry-ruby.svg)](https://rubygems.org/gems/sentry-ruby/) |
| [![Gem Version](https://img.shields.io/gem/v/sentry-rails?label=sentry-rails)](https://rubygems.org/gems/sentry-rails) | [![Build Status](https://github.com/getsentry/sentry-ruby/workflows/sentry-rails%20Test/badge.svg)](https://github.com/getsentry/sentry-ruby/actions/workflows/sentry_rails_test.yml) | [![Coverage Status](https://img.shields.io/codecov/c/github/getsentry/sentry-ruby/master?logo=codecov)](https://codecov.io/gh/getsentry/sentry-ruby/branch/master) | [![Downloads](https://img.shields.io/gem/dt/sentry-rails.svg)](https://rubygems.org/gems/sentry-rails/) |
| [![Gem Version](https://img.shields.io/gem/v/sentry-sidekiq?label=sentry-sidekiq)](https://rubygems.org/gems/sentry-sidekiq) | [![Build Status](https://github.com/getsentry/sentry-ruby/workflows/sentry-sidekiq%20Test/badge.svg)](https://github.com/getsentry/sentry-ruby/actions/workflows/sentry_sidekiq_test.yml) | [![Coverage Status](https://img.shields.io/codecov/c/github/getsentry/sentry-ruby/master?logo=codecov)](https://codecov.io/gh/getsentry/sentry-ruby/branch/master) | [![Downloads](https://img.shields.io/gem/dt/sentry-sidekiq.svg)](https://rubygems.org/gems/sentry-sidekiq/) |
| [![Gem Version](https://img.shields.io/gem/v/sentry-delayed_job?label=sentry-delayed_job)](https://rubygems.org/gems/sentry-delayed_job) | [![Build Status](https://github.com/getsentry/sentry-ruby/workflows/sentry-delayed_job%20Test/badge.svg)](https://github.com/getsentry/sentry-ruby/actions/workflows/sentry_delayed_job_test.yml) | [![Coverage Status](https://img.shields.io/codecov/c/github/getsentry/sentry-ruby/master?logo=codecov)](https://codecov.io/gh/getsentry/sentry-ruby/branch/master) | [![Downloads](https://img.shields.io/gem/dt/sentry-delayed_job.svg)](https://rubygems.org/gems/sentry-delayed_job/) |
| [![Gem Version](https://img.shields.io/gem/v/sentry-resque?label=sentry-resque)](https://rubygems.org/gems/sentry-resque) | [![Build Status](https://github.com/getsentry/sentry-ruby/workflows/sentry-resque%20Test/badge.svg)](https://github.com/getsentry/sentry-ruby/actions/workflows/sentry_resque_test.yml) | [![Coverage Status](https://img.shields.io/codecov/c/github/getsentry/sentry-ruby/master?logo=codecov)](https://codecov.io/gh/getsentry/sentry-ruby/branch/master) | [![Downloads](https://img.shields.io/gem/dt/sentry-resque.svg)](https://rubygems.org/gems/sentry-resque/) |




## Migrate From sentry-raven

**The old `sentry-raven` client has entered maintenance mode and was moved to [here](https://github.com/getsentry/sentry-ruby/tree/master/sentry-raven).**

If you're using `sentry-raven`, we recommend you to migrate to this new SDK. You can find the benefits of migrating and how to do it in our [migration guide](https://docs.sentry.io/platforms/ruby/migration/).

## Requirements

We test on Ruby 2.4, 2.5, 2.6, 2.7, and 3.0 at the latest patchlevel/teeny version. We also support JRuby 9.0.

If you use self-hosted Sentry, please also make sure its version is above `20.6.0`.

## Getting Started

### Install

```ruby
gem "sentry-ruby"
```

and depends on the integrations you want to have, you might also want to install these:

```ruby
gem "sentry-rails"
gem "sentry-sidekiq"
gem "sentry-delayed_job"
gem "sentry-resque"
```

### Configuration

You can use `Sentry.init` to initialize and configure your SDK:

```ruby
Sentry.init do |config|
  config.dsn = "MY_DSN"
end

```

To learn more about available configuration options, please visit the [official documentation](https://docs.sentry.io/platforms/ruby/configuration/options/).

### Performance Monitoring

You can activate [performance monitoring](https://docs.sentry.io/platforms/ruby/performance) by enabling traces sampling:

```ruby
Sentry.init do |config|
  # set a uniform sample rate between 0.0 and 1.0
  config.traces_sample_rate = 0.2
  # you can also use traces_sampler for more fine-grained sampling
  # please click the link below to learn more
end
```

To learn more about sampling transactions, please visit the [official documentation](https://docs.sentry.io/platforms/ruby/configuration/sampling/#configuring-the-transaction-sample-rate).

### Integrations

- [Rack](https://docs.sentry.io/platforms/ruby/guides/rack/)
- [Rails](https://docs.sentry.io/platforms/ruby/guides/rails/)
- [Sidekiq](https://docs.sentry.io/platforms/ruby/guides/sidekiq/)
- [DelayedJob](https://docs.sentry.io/platforms/ruby/guides/delayed_job/)
- [Resque](https://docs.sentry.io/platforms/ruby/guides/resque/)

```ruby
require 'sentry-ruby'

Sentry.init do |config|
  config.dsn = 'https://examplePublicKey@o0.ingest.sentry.io/0'

  # To activate performance monitoring, set one of these options.
  # We recommend adjusting the value in production:
  config.traces_sample_rate = 0.5
  # or
  config.traces_sampler = lambda do |context|
    true
  end
end

use Sentry::Rack::CaptureExceptions
```

Otherwise, Sentry you can always use the capture helpers manually

```ruby
Sentry.capture_message("hello world!")

begin
  1 / 0
rescue ZeroDivisionError => exception
  Sentry.capture_exception(exception)
end
```

We also provide integrations with popular frameworks/libraries with the related extensions:

- [sentry-rails](https://github.com/getsentry/sentry-ruby/tree/master/sentry-rails)
- [sentry-sidekiq](https://github.com/getsentry/sentry-ruby/tree/master/sentry-sidekiq)
- [sentry-delayed_job](https://github.com/getsentry/sentry-ruby/tree/master/sentry-delayed_job)

### More configuration

You're all set - but there's a few more settings you may want to know about too!

#### Logging with ActiveJob

By default, `Sentry::SendEventJob` will omit its arguments, since it amounts to a large and noisy Hash, which the Sentry frontend is designed to parse.
If you want the arguments to be logged, `ApplicationJob.log_sentry_arguments?` must be truthy.

For example, the following `ApplicationJob` will only log Sentry arguments if ActiveJob's logger's level is debug or lower (i.e. more verbose).

```ruby
class ApplicationJob < ActiveJob::Base
  def self.log_sentry_arguments?
    logger.level <= ::Logger::DEBUG
  end
end
```

#### Blocking v.s. Non-blocking

`sentry-ruby` sends events asynchronously by default. The functionality works like this:

1. When the SDK is initialized, a `Sentry::BackgroundWorker` will be initialized too.
2. When an event is passed to `Client#capture_event`, instead of sending it directly with `Client#send_event`, we'll let the worker do it.
3. The worker will have a number of threads. And the one of the idle threads will pick the job and call `Client#send_event`.
  - If all the threads are busy, new jobs will be put into a queue, which has a limit of 30.
  - If the queue size is exceeded, new events will be dropped.

However, if you still prefer to use your own async approach, that's totally fine. If you have `config.async` set, the worker won't initialize a thread pool and won't be used either.

##### About `Sentry::BackgroundWorker`

- The worker is built on top of the [concurrent-ruby](https://github.com/ruby-concurrency/concurrent-ruby) gem's [ThreadPoolExecutor](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ThreadPoolExecutor.html), which is also used by Rails ActiveJob's async adapter. This should minimize the risk of messing up client applications with our own thread pool implementaion.

This functionality also introduces a new `background_worker_threads` config option. It allows you to decide how many threads should the worker hold. By default, the value will be the number of the processors your machine has. For example, if your machine has 4 processors, the value would be 4.

Of course, you can always override the value to fit your use cases, like

```ruby
config.background_worker_threads = 5 # the worker will have 5 threads for sending events
```

You can also disable this new non-blocking behaviour by giving a `0` value:

```ruby
config.background_worker_threads = 0 # all events will be sent synchronously
```
### Enriching Events

- [Add more data to the current scope](https://docs.sentry.io/platforms/ruby/guides/rack/enriching-events/scopes/)
- [Add custom breadcrumbs](https://docs.sentry.io/platforms/ruby/guides/rack/enriching-events/breadcrumbs/)
- [Add contextual data](https://docs.sentry.io/platforms/ruby/guides/rack/enriching-events/context/)
- [Add tags](https://docs.sentry.io/platforms/ruby/guides/rack/enriching-events/tags/)

## Resources

* [![Ruby docs](https://img.shields.io/badge/documentation-sentry.io-green.svg?label=ruby%20docs)](https://docs.sentry.io/platforms/ruby/)
* [![Forum](https://img.shields.io/badge/forum-sentry-green.svg)](https://forum.sentry.io/c/sdks)
* [![Discord Chat](https://img.shields.io/discord/621778831602221064?logo=discord&logoColor=ffffff&color=7389D8)](https://discord.gg/PXa5Apfe7K)
* [![Stack Overflow](https://img.shields.io/badge/stack%20overflow-sentry-green.svg)](https://stackoverflow.com/questions/tagged/sentry)
* [![Twitter Follow](https://img.shields.io/twitter/follow/getsentry?label=getsentry&style=social)](https://twitter.com/intent/follow?screen_name=getsentry)
