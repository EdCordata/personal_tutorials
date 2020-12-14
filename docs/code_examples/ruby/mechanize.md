# Mechanize


#### Basic Usage
```ruby
agent = ::Mechanize.new

response = agent.get(url)    # get(uri, parameters = [], referer = nil, headers = {})
response = agent.post(url)   # post(uri, query = {}, headers = {})
response = agent.delete(uri) # delete(url, query_params = {}, headers = {})

status   = agent.history.map { |x| x.code.to_i }.last
source   = response.body
last_url = response.uri.to_s
```


#### Fix for windows error `uninitialized constant Process::RLIMIT_NOFILE`
```bash
gem uninstall net-http-persistent
gem install net-http-persistent -v 2.9.4
```


### Disable SSL
```ruby
agent = ::Mechanize.new

agent.agent.http.verify_mode = OpenSSL::SSL::VERIFY_NONE
```


#### Set User-Agent
```ruby
agent = ::Mechanize.new

# Set User-Agent with built-in aliases
# 'Linux Firefox', 'Linux Konqueror', 'Linux Mozilla', 'Mac Firefox', 'Mac Mozilla', 'Mac Safari 4', 'Mac Safari', 'Windows Chrome',
# 'Windows IE 6', 'Windows IE 7', 'Windows IE 8', 'Windows IE 9', 'Windows IE 10', 'Windows IE 11', 'Windows Edge', 'Windows Mozilla',
# 'Windows Firefox', 'iPhone', 'iPad', 'Android'
agent.user_agent_alias = 'Mac Safari'

# Set user-agent manually
agent.user_agent = 'Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/33.0.1750.117 Safari/537.36'
```


#### Headers
```ruby
agent = ::Mechanize.new

# Set Headers before connection
agent.pre_connect_hooks << lambda { |agent, request| request['X-Requested-With'] = 'XMLHttpRequest' } # get headers

# Get headers after request
response  = agent.get('url')
response.header # => { 'NAME' => '..' }
```


#### Proxy
```ruby
agent = ::Mechanize.new
agent.set_proxy('example.com', port = nil, user = nil, pass = nil)
```


#### HTTP Basic Auth
```ruby
agent = ::Mechanize.new

username = ''
password = ''

agent.add_auth('http://example.com', username, password)
# OR
agent.pre_connect_hooks << lambda do |agent, request| 
  request["Authorization"] = "Basic #{::Base64.strict_encode64(username + ':' + password)}"
end
```


#### Bearer Auth
```ruby
agent = ::Mechanize.new

token = ''

agent.pre_connect_hooks << lambda { |agent, request| request['Authorization'] = "Bearer #{token}" }
```


### Get Cookies
```ruby
agent = ::Mechanize.new

agent.cookies.each do |cookie|
  # cookie methods:
  # [name, value, domain, for_domain, path, secure, httponly, expires, created_at, accessed_at, origin, secure]
end
```


### Set Cookies
```ruby
agent = ::Mechanize.new

cookie = ::Mechanize::Cookie.new(domain: '.mydomain.com', 
  name: 'name', 
  value: 'value', 
  path: '/', 
  expires: (::Date.today + 1).to_s
)

agent.cookie_jar << cookie
```


### Download a File (without loading it into memory)
```ruby
agent = ::Mechanize.new
agent.pluggable_parser.default = ::Mechanize::Download
agent.get('url').save('test.zip')
```
