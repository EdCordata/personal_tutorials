# Active Record without Rails

```ruby
source 'https://rubygems.org'

gem 'activerecord'
gem 'sqlite3'
```

```ruby
require 'active_record'


# setup connection
# --------------------------------------------------------

ActiveRecord::Base.establish_connection(
  adapter:  'sqlite3',
  database: 'test_db.db'
)

# or

ActiveRecord::Base.establish_connection(
  adapter:  'mysql2',
  host:     'localhost',
  username: 'root',
  password: 'develop',
  database: 'test_db'
)

# or

ActiveRecord::Base.establish_connection(
  YAML::load(
    File.open('database.yaml')
  )
)

# --------------------------------------------------------


# setup logs
# --------------------------------------------------------

# Set up STDOUT or provide a filename like 'log.txt'
ActiveRecord::Base.logger = ActiveSupport::Logger.new(STDOUT)

# To disable the ANSI color output:
ActiveSupport::LogSubscriber.colorize_logging = true

# --------------------------------------------------------


# setup migrations
# --------------------------------------------------------
class CreateProductsTable < ActiveRecord::Migration[5.2]

  def up
    unless ActiveRecord::Base.connection.table_exists?(:products)
      create_table :products do |t|
        t.string :name
        t.timestamps
      end
    end
  end


  def down
    drop_table :products
  end

end
# --------------------------------------------------------


# run migrations
# --------------------------------------------------------
CreateProductsTable.migrate(:up)
# --------------------------------------------------------


# setup models
# --------------------------------------------------------
class Product < ActiveRecord::Base

  validates :name,
            presence:   true,
            uniqueness: { case_sensitive: true }

end
# --------------------------------------------------------


# perform transactions
# --------------------------------------------------------
ActiveRecord::Base.transaction do
  # Product.create!(name: '123')
  # multiple actions to ensure all are success
end
# --------------------------------------------------------
```
