# Blorgh
Short description and motivation.

## Usage
How to use my plugin.

## Installation
Add this line to your application's Gemfile:

https://www.bignerdranch.com/blog/intro-to-rails-engines/

```ruby
gem 'blorgh'
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install blorgh
```

## Contributing
Contribution directions go here.

## License
The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

### Tutorials Used
+ https://guides.rubyonrails.org/engines.html

+ https://csil-git1.cs.surrey.sfu.ca/ypleung/cmpt276ass2/blob/master/vendor/bundle/ruby/2.3.0/gems/rails-4.2.5/guides/source/engines.md


### Fixed the error:
```
blorgh.gemspec is not valid. Please fix this gemspec. (Gem::InvalidSpecificationException) The validation error was '"FIXME" or "TODO" is not a description'
```
by deleting the TODOs
```$:.push File.expand_path("lib", __dir__)

# Maintain your gem's version:
require "blorgh/version"

# Describe your gem and declare its dependencies:
Gem::Specification.new do |s|
  s.name        = "blorgh"
  s.version     = Blorgh::VERSION
  s.authors     = ["myname"]
  s.email       = ["myactualemail@email.com"]
  s.homepage    = ""
  s.summary     = ": Summary of Blorgh."
  s.description = ": Description of Blorgh."
  s.license     = "MIT"

  s.files = Dir["{app,config,db,lib}/**/*", "MIT-LICENSE", "Rakefile", "README.md"]

  s.add_dependency "rails", "~> 5.2.1"

  s.add_development_dependency "sqlite3"
end
```

### Error: `ActionView::Template::Error (Asset was not declared to be precompiled in production.
`
#### The Fix
https://stackoverflow.com/questions/35683185/rails-sprocketsrailshelperassetnotprecompiled-in-development

I Changed: This:  
`config.assets.debug = true`  
To This:  
`config.assets.check_precompiled_asset = false`

**`test/dummy/config/environments/development.rb`**
```
Rails.application.configure do

  config.cache_classes = false
  config.eager_load = false
  config.consider_all_requests_local = true

  if Rails.root.join('tmp', 'caching-dev.txt').exist?
    config.action_controller.perform_caching = true

    config.cache_store = :memory_store
    config.public_file_server.headers = {
      'Cache-Control' => "public, max-age=#{2.days.to_i}"
    }
  else
    config.action_controller.perform_caching = false

    config.cache_store = :null_store
  end

  config.active_storage.service = :local
  config.action_mailer.raise_delivery_errors = false
  config.action_mailer.perform_caching = false
  config.active_support.deprecation = :log
  config.active_record.migration_error = :page_load
  config.active_record.verbose_query_logs = true
  config.assets.check_precompiled_asset = false
  config.assets.quiet = true

end
```

### Change into the test/dummy directory
$ `cd test/dummy`  
and then run  
$ `rails s`  