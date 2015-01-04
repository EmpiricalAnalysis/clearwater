# Clearwater

Clearwater is a browser MVC framework, similar to Ember.js or Backbone.js. The primary difference is that Clearwater is written in Ruby and compiled using Opal.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'clearwater', github: 'jgaskins/clearwater'
```

And then execute:

    $ bundle

## Usage

Clearwater targets the Rails asset pipeline, so it will work best in a Rails app. It may work fine with other server-side web frameworks, but I haven't tried it yet.

### Create your application

#### app/assets/javascripts/application.rb

```ruby
# These three just bootstrap Opal and load the jQuery bindings
require 'opal'
require 'jquery'
require 'opal-jquery'

# Pick one of these two depending on which template engine you like most.
require 'opal-haml'
require 'opal-slim'

# Load Clearwater
require 'clearwater/application'

# You have to load your templates.
# Alternatively: require_tree './templates'
require 'templates/application'

class ApplicationController < Clearwater::Controller
  view { ApplicationView.new }
end

class ApplicationView < Clearwater::View
  element '#app'
  template 'application'
end

MyApp = Clearwater::Application.new(
  controller: ApplicationController.new
)

Document.ready? do
  MyApp.call
end
```

#### app/assets/javascripts/templates/application.slim

```slim
h1 This is a Ruby app!
```

## Known issues

- Back button is broken.
- Cmd-clicking a link doesn't open in a new tab
- Click events on links that don't begin with `%r{(\w+)://}` are trapped by Clearwater
  - Protocol-relative hrefs (such as `//google.com/`) will be trapped.
  - No way to indicate a link we *don't* want the app to handle, even if it is host-relative.

## Contributing

1. Fork it ( https://github.com/jgaskins/clearwater/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request