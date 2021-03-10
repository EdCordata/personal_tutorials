# Ruby - Nokogiri


#### Basic Usage
```ruby
require 'nokogiri'

# remote source
source = open('url')
doc    = ::Nokogiri.new

# HTML snippet (without html and body)
doc = ::Nokogiri::HTML::fragment('<div>content</div>', 'UTF-8')

# XML
doc = ::Nokogiri::XML('<?xml version="1.0" encoding="utf-8"?></xml>')
```


#### Find Elements
```ruby
links = doc.css('a')
link  = doc.at_css('a') # same as doc.css('a').first
```


#### Get Element Info
```ruby
doc = Nokogiri::HTML::fragment('<a href="example.com" id="a" class="b"> <span>content</span> </a>') 
link = doc.at_css('a')

# get attributes
link.attribute('id')    # => 'a'
link.attribute('class') # => 'b'
link.attribute('href')  # => 'example.com'

# get all attributes 
link.attribute_nodes

# get tag name
link.name # => 'a'

# Get link content as text
link.text # => 'content'

# get HTML
link.inner_html # => '<span>content</span>'
link.to_html    # => '<a href="example.com" id="a" class="b"><span>content</span></a>'

# get path to this element as CSS expression
link.css_path 
```


#### Traversion
```ruby
el = doc.css('.class').first

el.ancestors
el.parent
el.children
el.next
el.previous
```


#### Create & Insert New Elements
```ruby
# create new element
el = ::Nokogiri::XML::Node.new('div')
el.attr['id'] = 'some-id'
el.inner_html = '<p>content</p>'

el. # => '<div><p>content</p></div>'

# adds #some-id after element #one
doc.css('#one').after(el)
doc.css('#one').add_next_sibling(el)

# adds #some-id before element #one
doc.css('#one').before(el)
doc.css('#one').add_previous_sibling(el)

# adds #some-id as #one child
doc.css('#one').add_child(el)

# Replace #one with #some-id
doc.css('#one').replace(el)
doc.css('#one').swap(el) # same as .replace, but returns self to support chaining
```


#### Remove Elements
```ruby
doc.css('a').each { |a| a.remove } # remove all links
```


#### Copy element to new variable
```ruby
doc.css_at('a').clone
```
