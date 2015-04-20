# OmniAuth Clever

Unofficial OmniAuth strategy for [Clever SSO OAuth2](https://dev.clever.com/sso) integration.

## Installation

Add the gem to your application's Gemfile:

    gem 'omniauth-clever', '~> 1.2.0'

And then execute:

    $ bundle

## Usage

OmniAuth Clever is Rack Middleware in the OmniAuth convention. See the
[OmniAuth 1.0 docs](https://github.com/intridea/omniauth) for more information.

Follow the Clever OAuth docs to register your application, set callback URLs,
and get a client ID and client secret.

Example: In `config/initializers/omniauth.rb`, do:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :clever, ENV['CLEVER_CLIENT_ID'], ENV['CLEVER_CLIENT_SECRET']
end
```

## Configuring

To be able to set the optional `district_id` parameter on a
per-request basis, passing this params to your `/auth/clever` url, use
this in the initializer instead:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :clever, ENV['CLEVER_CLIENT_ID'], ENV['CLEVER_CLIENT_SECRET'],
           :setup => lambda { |env|
             params = Rack::Utils.parse_query(env['QUERY_STRING'])
             env['omniauth.strategy'].options[:client_options][:district_id] = params['district_id']
           }
end
```

## Testing

This strategy can be and has been tested with the [omniauth-test-harness](https://github.com/PracticallyGreen/omniauth-test-harness).

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

MIT. See LICENSE.txt.

## Thank yous

Thank you to the [Clever](https://github.com/Clever/) team for their awesome
product and always being helpful with any issues. Thank you to [Think Through
Math](https://github.com/thinkthroughmath) for dedicating time for the tech
team to make open source contributions such as this. Thank you to [StudyPad] for helping bringing the strategy up to date.

And, of course. thank you to [Omniauth](https://github.com/intridea/omniauth)
for making it so easy create this gem!
