# Migration

https://edgeguides.rubyonrails.org/active_record_migrations.html
- = a script that tells Rails how you want to set up or change a database.
	- each migration as being a new 'version' of the database
	- A schema starts off with nothing in it, and each migration modifies it to add or remove tables, columns, or entries.
- Migrations will be stored in `db/migration` directory.
- Active Record will update your `db/schema.rb` file to match the up-to-date structure of your database
- To actually create the table, you'd run `bin/rails db:migrate`, and to roll it back, `bin/rails db:rollback`.
	- Here is a mgiration that creates a table. Note that the below code is database-agnostic: it will run in MySQL, PostgreSQL, Oracle, and others.
		```ruby
		class CreatePublications < ActiveRecord::Migration[6.0]
		  def change
			create_table :publications do |t|
			  t.string :title
			  t.text :description
			  t.references :publication_type
			  t.integer :publisher_id
			  t.string :publisher_type
			  t.boolean :single_issue

			  # the timestamps macro adds two columns, `created_at` and `updated_at`.
			  t.timestamps
			end
			add_index :publications, :publication_type_id
		  end
		end
		```

<hr>

#### adding a new column:

```ruby
$ bin/rails generate migration AddDetailsToProducts part_number:string price:decimal
```

will generate: 
```ruby
class AddDetailsToProducts < ActiveRecord::Migration[6.0]
  def change
    add_column :products, :part_number, :string
    add_column :products, :price, :decimal
  end
end
```

#### adding a new table (create_table): 
```ruby
$ bin/rails generate migration CreateProducts name:string part_number:string
```

will generate:
```ruby
class CreateProducts < ActiveRecord::Migration[6.0]
  def change
    create_table :products do |t|
      t.string :name
      t.string :part_number

      t.timestamps
    end
  end
end
```

#### add_reference:
```ruby
$ bin/rails generate migration AddUserRefToProducts user:references
```
creates:
```ruby
class AddUserRefToProducts < ActiveRecord::Migration[6.0]
  def change
    add_reference :products, :user, foreign_key: true
  end
end
```

#### CreateJoinTable
The migration method [`create_join_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-create_join_table) creates an HABTM (has and belongs to many) join table. A typical use would be:
```ruby
create_join_table :products, :categories
```
```ruby
$ bin/rails generate migration CreateJoinTableCustomerProduct customer product
```
creates:
```ruby
class CreateJoinTableCustomerProduct < ActiveRecord::Migration[6.0]
  def change
    create_join_table :customers, :products do |t|
      # t.index [:customer_id, :product_id]
      # t.index [:product_id, :customer_id]
    end
  end
end
```

#### options
```sql
create_table :products, options: "ENGINE=BLACKHOLE" do |t|
  t.string :name, null: false
end
```
will append `ENGINE=BLACKHOLE` to the SQL statement used to create the table.

#### Changing a table (change_table):
```ruby
change_table :products do |t|
  t.remove :description, :name
  t.string :part_number
  t.index :part_number
  t.rename :upccode, :upc_code
end
```
removes the `description` and `name` columns, creates a `part_number` string column and adds an index on it. Finally it renames the `upccode` column.

#### Changing a column (change_column):
```ruby
change_column :products, :part_number, :text
```
This changes the column `part_number` on products table to be a `:text` field. Note that `change_column` command is irreversible.

#### the Change method
The `change` method is the primary way of writing migrations. It works for the majority of cases, where Active Record knows how to reverse the migration automatically. Currently, the `change` method supports only these migration definitions:

-   [`add_column`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_column)
-   [`add_foreign_key`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_foreign_key)
-   [`add_index`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_index)
-   [`add_reference`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_reference)
-   [`add_timestamps`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_timestamps)
-   [`change_column_default`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-change_column_default) (must supply a `:from` and `:to` option)
-   [`change_column_null`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-change_column_null)
-   [`create_join_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-create_join_table)
-   [`create_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-create_table)
-   `disable_extension`
-   [`drop_join_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-drop_join_table)
-   [`drop_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-drop_table) (must supply a block)
-   `enable_extension`
-   [`remove_column`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_column) (must supply a type)
-   [`remove_foreign_key`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_foreign_key) (must supply a second table)
-   [`remove_index`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_index)
-   [`remove_reference`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_reference)
-   [`remove_timestamps`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_timestamps)
-   [`rename_column`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-rename_column)
-   [`rename_index`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-rename_index)
-   [`rename_table`](https://edgeapi.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-rename_table)

<hr>

## Schema
- By default, Rails generates `db/schema.rb` which attempts to capture the current state of your database schema.
- It tends to be faster and less error prone to create a new instance of your application's database by loading the schema file via `bin/rails db:schema:load` than it is to replay the entire migration history.
- Example schema file:
```ruby
ActiveRecord::Schema.define(version: 2008_09_06_171750) do
  create_table "authors", force: true do |t|
    t.string   "name"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

  create_table "products", force: true do |t|
    t.string   "name"
    t.text     "description"
    t.datetime "created_at"
    t.datetime "updated_at"
    t.string   "part_number"
  end
end
```

Schema dumping in SQL:
When the schema format is set to `:sql`, the database structure will be dumped using a tool specific to the database into `db/structure.sql`. For example, for PostgreSQL, the `pg_dump` utility is used. For MySQL and MariaDB, this file will contain the output of `SHOW CREATE TABLE` for the various tables.

To load the schema from `db/structure.sql`, run `bin/rails db:schema:load`. Loading this file is done by executing the SQL statements it contains. By definition, this will create a perfect copy of the database's structure.