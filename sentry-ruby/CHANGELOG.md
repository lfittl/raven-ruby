# Changelog

## Unreleased

### Bug Fixes

- Ignore invalid values for sentry-trace header that don't match the required format [#1265](https://github.com/getsentry/sentry-ruby/pull/1265)
- Correctly call sampled state initialization logic when capturing sentry-trace [#1265](https://github.com/getsentry/sentry-ruby/pull/1265)
  - Previously the span's sampled state was always set to nil when the sentry-trace header was set,
    which caused child spans to not be reported

## 4.2.0

### Features

- Add configuration option for trusted proxies [#1126](https://github.com/getsentry/sentry-ruby/pull/1126)

```ruby
config.trusted_proxies = ["2.2.2.2"] # this ip address will be skipped when computing users' ip addresses
```

- Add ThreadsInterface [#1178](https://github.com/getsentry/sentry-ruby/pull/1178)

<img width="1029" alt="an exception event that has the new threads interface" src="https://user-images.githubusercontent.com/5079556/103459223-98b64c00-4d48-11eb-9ebb-ee58f15e647e.png">

- Support `config.before_breadcrumb` [#1253](https://github.com/getsentry/sentry-ruby/pull/1253)

```ruby
# this will be called before every breadcrumb is added to the breadcrumb buffer
# you can use it to
# - remove the data you don't want to send
# - add additional info to the data
config.before_breadcrumb = lambda do |breadcrumb, hint|
  breadcrumb.message = "foo"
  breadcrumb
end
```

- Add ability to have many post initialization callbacks [#1261](https://github.com/getsentry/sentry-ruby/pull/1261)

### Bug Fixes

- Inspect exception cause by default & don't exclude ActiveJob::DeserializationError [#1180](https://github.com/getsentry/sentry-ruby/pull/1180)
  - Fixes [#1071](https://github.com/getsentry/sentry-ruby/issues/1071)

## 4.1.6

- Don't detect project root for Rails apps [#1243](https://github.com/getsentry/sentry-ruby/pull/1243)
- Separate individual breadcrumb's data serialization [#1250](https://github.com/getsentry/sentry-ruby/pull/1250)
- Capture sentry-trace with the correct http header key [#1260](https://github.com/getsentry/sentry-ruby/pull/1260)

## 4.1.5

- Serialize event hint before passing it to the async block [#1231](https://github.com/getsentry/sentry-ruby/pull/1231)
  - Fixes [#1227](https://github.com/getsentry/sentry-ruby/issues/1227)
- Require the English library [#1233](https://github.com/getsentry/sentry-ruby/pull/1233) (by @dentarg)
- Allow `Sentry.init` without block argument [#1235](https://github.com/getsentry/sentry-ruby/pull/1235) (by @sue445)

## 4.1.5-beta.1

- No change

## 4.1.5-beta.0

- Inline global method [#1213](https://github.com/getsentry/sentry-ruby/pull/1213) (by @tricknotes)
- Event message and exception message should have a size limit [#1221](https://github.com/getsentry/sentry-ruby/pull/1221)
- Add sentry-ruby-core as a more flexible option [#1226](https://github.com/getsentry/sentry-ruby/pull/1226)

## 4.1.4

- Fix headers serialization for sentry-ruby [#1197](https://github.com/getsentry/sentry-ruby/pull/1197) (by @moofkit)
- Support capturing "sentry-trace" header from the middleware [#1205](https://github.com/getsentry/sentry-ruby/pull/1205)
- Document public APIs on the Sentry module [#1208](https://github.com/getsentry/sentry-ruby/pull/1208)
- Check the argument type of capture_exception and capture_event helpers [#1209](https://github.com/getsentry/sentry-ruby/pull/1209)

## 4.1.3

- rm reference to old constant (from Rails v2.2) [#1184](https://github.com/getsentry/sentry-ruby/pull/1184)
- Use copied env in events [#1186](https://github.com/getsentry/sentry-ruby/pull/1186)
  - Fixes [#1183](https://github.com/getsentry/sentry-ruby/issues/1183)
- Refactor RequestInterface [#1187](https://github.com/getsentry/sentry-ruby/pull/1187)
- Supply event hint to async callback when possible [#1189](https://github.com/getsentry/sentry-ruby/pull/1189)
  - Fixes [#1188](https://github.com/getsentry/sentry-ruby/issues/1188)
- Refactor stacktrace parsing and increase test coverage [#1190](https://github.com/getsentry/sentry-ruby/pull/1190)
- Sentry.send_event should also take a hint [#1192](https://github.com/getsentry/sentry-ruby/pull/1192)

## 4.1.2

- before_send callback shouldn't be applied to transaction events [#1167](https://github.com/getsentry/sentry-ruby/pull/1167)
- Transaction improvements [#1170](https://github.com/getsentry/sentry-ruby/pull/1170)
- Support Ruby 3 [#1172](https://github.com/getsentry/sentry-ruby/pull/1172)
- Add Integrable module [#1177](https://github.com/getsentry/sentry-ruby/pull/1177)

## 4.1.1

- Fix NoMethodError when sending is not allowed [#1161](https://github.com/getsentry/sentry-ruby/pull/1161)
- Add notification for users who still use deprecated middlewares [#1160](https://github.com/getsentry/sentry-ruby/pull/1160)
- Improve top-level api safety [#1162](https://github.com/getsentry/sentry-ruby/pull/1162)

## 4.1.0

- Separate rack integration [#1138](https://github.com/getsentry/sentry-ruby/pull/1138)
  - Fixes [#1136](https://github.com/getsentry/sentry-ruby/pull/1136)
- Fix event sampling [#1144](https://github.com/getsentry/sentry-ruby/pull/1144)
- Merge & rename 2 Rack middlewares [#1147](https://github.com/getsentry/sentry-ruby/pull/1147)
  - Fixes [#1153](https://github.com/getsentry/sentry-ruby/pull/1153)
  - Removed `Sentry::Rack::Tracing` middleware and renamed `Sentry::Rack::CaptureException` to `Sentry::Rack::CaptureExceptions`.
- Deep-copy spans [#1148](https://github.com/getsentry/sentry-ruby/pull/1148)
- Move span recorder related code from Span to Transaction [#1149](https://github.com/getsentry/sentry-ruby/pull/1149)
- Check SDK initialization before running integrations [#1151](https://github.com/getsentry/sentry-ruby/pull/1151)
  - Fixes [#1145](https://github.com/getsentry/sentry-ruby/pull/1145)
- Refactor transport [#1154](https://github.com/getsentry/sentry-ruby/pull/1154)
- Implement non-blocking event sending [#1155](https://github.com/getsentry/sentry-ruby/pull/1155)
  - Added `background_worker_threads` configuration option.

### Noticeable Changes

#### Middleware Changes

`Sentry::Rack::Tracing` is now removed. And `Sentry::Rack::CaptureException` has been renamed to `Sentry::Rack::CaptureExceptions`.

#### Events Are Sent Asynchronously

`sentry-ruby` now sends events asynchronously by default. The functionality works like this: 

1. When the SDK is initialized, a `Sentry::BackgroundWorker` will be initialized too.
2. When an event is passed to `Client#capture_event`, instead of sending it directly with `Client#send_event`, we'll let the worker do it.
3. The worker will have a number of threads. And the one of the idle threads will pick the job and call `Client#send_event`.
    - If all the threads are busy, new jobs will be put into a queue, which has a limit of 30.
    - If the queue size is exceeded, new events will be dropped.

However, if you still prefer to use your own async approach, that's totally fine. If you have `config.async` set, the worker won't initialize a thread pool and won't be used either.

This functionality also introduces a new `background_worker_threads` config option. It allows you to decide how many threads should the worker hold. By default, the value will be the number of the processors your machine has. For example, if your machine has 4 processors, the value would be 4.

Of course, you can always override the value to fit your use cases, like

```ruby
config.background_worker_threads = 5 # the worker will have 5 threads for sending events
```

You can also disable this new non-blocking behaviour by giving a `0` value:

```ruby
config.background_worker_threads = 0 # all events will be sent synchronously
```

## 4.0.1

- Add rake integration: [1137](https://github.com/getsentry/sentry-ruby/pull/1137)
- Make Event's interfaces accessible: [1135](https://github.com/getsentry/sentry-ruby/pull/1135)
- ActiveSupportLogger should only record events that has a started time: [1132](https://github.com/getsentry/sentry-ruby/pull/1132)

## 4.0.0

- Only documents update for the official release and no API/feature changes.

## 0.3.0

- Major API changes: [1123](https://github.com/getsentry/sentry-ruby/pull/1123)
- Support event hint: [1122](https://github.com/getsentry/sentry-ruby/pull/1122)
- Add request-id tag to events: [1120](https://github.com/getsentry/sentry-ruby/pull/1120) (by @tvec)

## 0.2.0

- Multiple fixes and refactorings
- Tracing support

## 0.1.3

Fix require reference

## 0.1.2

- Fix: Fix async callback [1098](https://github.com/getsentry/sentry-ruby/pull/1098)
- Refactor: Some code cleanup [1100](https://github.com/getsentry/sentry-ruby/pull/1100)
- Refactor: Remove Event options [1101](https://github.com/getsentry/sentry-ruby/pull/1101)

## 0.1.1

- Feature: Allow passing custom scope to Hub#capture* helpers [1086](https://github.com/getsentry/sentry-ruby/pull/1086)

## 0.1.0

First version
