# Ruby - Mechanize


#### Initialize
```ruby
source 'https://rubygems.org'

gem 'poltergeist'
gem 'phantomjs'
gem 'capybara'
gem 'launchy' # to auto-open url's
```
```ruby
require 'launchy'
require 'phantomjs'
require 'capybara'
require 'capybara/poltergeist'

@session = nil

::Capybara.register_driver(:poltergeist) do |app|

  driver_options = {
    debug:             false,
    timeout:           60,
    js_errors:         false,
    window_size:       [1600, 1200],
    screen_size:       [1600, 1200],
    phantomjs:         ::Phantomjs.path,
    phantomjs_logger:  STDOUT,
    phantomjs_options: %w(
          --debug=false
          --ignore-ssl-errors=yes
          --web-security=false
          --ssl-protocol=any
          --proxy-type=none
          --load-images=no
        )
  }

  ::Capybara::Poltergeist::Driver.new(app, driver_options)
end

@session = ::Capybara::Session.new(:poltergeist)
```


#### Load URL
```ruby
@session.visit('url')
```


### Get HTML
```ruby
# Get HTML
source = @session.html

# Get Element HTML
@session.first('a')['innerHTML']
@session.first('a')['outerHTML'] 
```


### Find Elements
```ruby
@session.find('#id')
@session.all('.sel')

# Search within specific element
@session.within 'form#form-1' do
  @session.find('a')
end

# Find hidden elements
@session.find('#id', visible: true)
```


### Get Element Tag Name
```ruby
@session.first('a').tag_name 
```


#### Fill Input
```ruby
@session.first('input[type="text"]').set('test')
```


#### Fill Select
```ruby
@session.first('select#id').first("option[value='1']").select_option
```


#### Set Checkbox
```ruby
@session.first('input[type="checkbox"]').set(true)
@session.first('input[type="checkbox"]').set(false)
```


#### Set File Field
```ruby
# Single File
@session.first('input[type="file"]').set('test.png')

# Multiple Files
@session.attach_file('input_name', ['test.png'], make_visible: true, multiple: true) 
```


#### Inject & Execute JavaScript
```ruby
@session.execute_script("document.querySelector('body').innerHTML = 'works'")
```


#### Click Buttons & Links
```ruby
@session.click_button('buttons text')
@session.click_button(class: 'el-class')
@session.click_button(id:    'el-id')
@session.find('#id').click
```


#### Debug
```ruby
@session.save_and_open_page       # requires launchy
@session.save_and_open_screenshot # requires launchy     
@session.save_screenshot('xxx.png', full: true)
@session.save_page('xxx.html')
```
