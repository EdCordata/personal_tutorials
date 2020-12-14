# Docker - Sinatra


#### Files:
* Gemfile
* app.rb
* config.ru
* docker-composer.yml


#### `Gemfile`:
```ruby
source 'https://rubygems.org'

gem 'sinatra'
```


#### `app.rb`:
```ruby
require 'sinatra'

get '/' do
  'Hello world!'
end
```


#### `config.ru`:
```ruby
require './app'
run Sinatra::Application
```


#### `docker-compose.yml`:
```yaml
version: "3.7"

services:


  # sinatra_app
  # ----------------------------------------------------------------------
  sinatra_app:
    image:       'ruby:2.7.0'
    ports:       [ '3000:3000' ]
    volumes:     [ '.:/app', 'bundle-cache:/usr/local/bundle' ]
    working_dir: '/app'

    # use this to "ssh" in to box with: docker-compose run --rm --service-ports sinatra_app
    # command: /bin/bash

    # use this to run the server
    command: bash -c 'bundle install && bundle exec rackup -p 3000 --host 0.0.0.0'
  # ----------------------------------------------------------------------


volumes:
  bundle-cache:
```
