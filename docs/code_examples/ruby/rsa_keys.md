# Ruby - Generating RSA keys & Encrypting/Decrypting data


#### Generate/Read key:
```ruby
require 'sshkey'
require 'json'
require 'jwt'

# Generate key
key = SSHKey.generate(type: 'RSA', bits: 2048, passphrase: "foobar")

# Read exsiting id_rsa file
key = SSHKey.new(File.read(File.expand_path("~/.ssh/id_rsa")), comment: "foo@bar.com")

# Read from private/public key string
key = SSHKey.new('private/public key string')
```


#### Extract info from keys
```ruby
puts key.private_key
# =>
# -----BEGIN RSA PRIVATE KEY-----
# MIIEpAIBAAKCAQEAnElbH+n...
# -----END RSA PRIVATE KEY-----

puts key.public_key
# =>
# -----BEGIN PUBLIC KEY-----
# MIIBIjANBgkqhkiG9w...
# -----END PUBLIC KEY-----

puts key.ssh_public_key
# =>
# ssh-rsa AAAAB3NzaC1yc2EAAAAD...

puts key.randomart
# =>
# +--[ RSA 2048]----+
# |o+ o..           |
# |..+.o            |
# | ooo             |
# |.++. o           |
# |+o+ +   S        |
# |.. + o .         |
# |  . + .          |
# |   . .           |
# |    Eo.          |
# +-----------------+
```


#### Encrypt:
```ruby
encoded_data = JWT.encode({test: 'data'}, key.key_object, 'RS256')

puts encoded_data
# =>
# eyJhbGciOiJSUzI1NiJ9.eyJ0ZXN0...
```


#### Decrypt
```ruby
decoded_data = JWT.decode(encoded_data, key.key_object, true, {algorithm: 'RS256'})

puts decoded_data.inspect
# =>
# [ {"test"=>"data"}, {"alg"=>"RS256"} ]
```
