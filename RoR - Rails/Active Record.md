# Active Record[^1]
- the interface that Rails gives you between the database and your application. It lets you structure your data models in a logical and nearly plain-English way.
- Rails is actually seven Ruby gems that work harmoniously together. Active Record is, to put it inelegantly, the gem that takes care of all the database stuff. It’s known as an “ORM”. 
- **Object Relational Mapping** (ORM) lets you interact with SQL data (or any other data, as long as config/database.yml is gucci) as if they were Ruby objects.
<hr>


## Rails Models
- To store info about users, you create a database table called users. Then, you create a Rails model called User, which is just a Ruby file that inherits from Active Records  thus gets to use all the handy methods I was alluding to earlier like `all` and `find` and `create`.

- Application Record
	- One way to create a model is: 
			```
			class Product < ApplicationRecord
			```
	- `ApplicationRecord` inherits from `ActiveRecord::Base`, which defines a number of helpful methods.
		

- After creating the db by `$ rails db:create`, you can make the model by `$ rails generate model YourModelNameHere`.
	- This does two things: 
	1.  **create model** - create a model file in `app/models` which is set up like you just learned above.
	2.  **migrate** - create a database table called “users” that has the appropriate columns. This is done using a migration file and then running the migration.
		- If you want to just do this step to modify rather than create new db, run `$ rails generate migration NameYourMigration`.

<hr>

## [[RoR Migration]]
https://edgeguides.rubyonrails.org/active_record_migrations.html
- = a script that tells Rails how you want to set up or change a database.
	- each migration as being a new 'version' of the database
	- A schema starts off with nothing in it, and each migration modifies it to add or remove tables, columns, or entries.
- Migrations will be stored in `db/migration` directory.
- Active Record will update your `db/schema.rb` file to match the up-to-date structure of your database

<hr>

## ORM / Creating and Writing Data
- CRUD - **C**reate, **R**ead, **U**pdate and **D**elete.

#### CREATE (.new or .create)

To create a new user:

```bash
u = User.new(name: "Sven", email: "sven@theodinproject.com")
u.save
```
is the same thing as

```bash
u = User.create(name: "Sven", email: "sven@theodinproject.com")
```

if a block is provided, both `create` and `new` will yield the new object to that block for initialization:
```ruby
user = User.new do |u|
  u.name = "David"
  u.occupation = "Code Artist"
end
```

#### READ (.all, .first, .where)
```ruby
# return a collection of all users
users = User.all
```
```ruby
# return the first user
users = User.first
```
```ruby
# return the first user named David
david = User.find_by(name: 'David')
```
```ruby
#find all users named David who are Code Artists and sort by created_at in reverse chronological order
users = User.where(name:'David', occupation:'Code Artists').order(created_at: :desc)
```

#### UPDATE (.update)
```ruby
user = User.find_by(name: 'David')
user.name = 'Dave'
user.save
```
a shorthand for above code is:
```ruby
user = User.find_by(name: 'David')
user.update(name: 'Dave')
```
When updating in bulk, use `update_all` class method:
```ruby
User.update_all "max_login_attempts = 3, must_change_password = true"
```

#### DELETE (.destroy)
```ruby
user = User.find_by(name: David)
user.destroy
```
```ruby
# find and delete all users named David
user.destroy_by(name: 'David')

# delete all users
User.destroy_all
```

<hr>

## Basic Validations
https://guides.rubyonrails.org/active_record_validations.html

- there are 3 layers of validations
	1. Javascript
		- immediate but user can easily circumvent it
	2. Server (model - e.g. User)
		- most validations can happen here
		- more secure but has to take full round-trip HTTP request
		- also, if your application scales up, it might cause problem if multiple instances of it on multiple servers. for example, two users requesting the same usernames at the same time.
	3. Database level
		- the only way to truly enforce constraints
		- You can use extra parameters passed to some of the migration methods like `add_index` to say `add_index :users, :username, unique: true`

```ruby
class User < ApplicationRecord
  validates :name, presence: true
end
```

```ruby
irb > user = User.new
irb > user.save # => false
irb > user.save! # => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
```

<hr>

## Basic Associations

- **one-to-many**: “has many / belongs to” association (a User `has_many` Post objects associated with it and a Post `belongs_to` a single User).
	- A book belongs person A. Or a book belongs to multiple people.
- **many-to-many**: "has and belongs to many" association.
	- A dog has favorite humans A and B. A human has favorite dogs Y and Z.
	- To keep track of all the relationships, tt actually requires you to create another table (a join table, or “through” table).

#### Convention Over Configuration[^2]
- Naming Conventions
	-   Model Class - Singular with the first letter of each word capitalized (e.g., `BookClub`).
	-   Database Table - Plural with underscores separating words (e.g., `book_clubs`).
	![[Screen Shot 2021-01-26 at 2.50.22 PM.png]]
-   Schema Conventions
	-   **Foreign Keys** -    These fields should be named following the pattern `singularized_table_name_id` (e.g., `item_id`, `order_id`). These are the fields that Active Record will look for when you create associations between your models.
	-   **Primary keys** \- By default, Active Record will use an integer column named `id` as the table's primary key (`bigint` for PostgreSQL and MySQL, `integer` for SQLite). When using [Active Record Migrations](https://guides.rubyonrails.org/active_record_migrations.html) to create your tables, this column will be automatically created.
	-   There are also some optional column names that will add additional features to Active Record instances:
		-   `created_at` \- Automatically gets set to the current date and time when the record is first created.
		-   `updated_at` \- Automatically gets set to the current date and time whenever the record is created or updated.
		-   `lock_version` \- Adds [optimistic locking](https://api.rubyonrails.org/v6.1.1/classes/ActiveRecord/Locking.html) to a model.
		-   `type` \- Specifies that the model uses [Single Table Inheritance](https://api.rubyonrails.org/v6.1.1/classes/ActiveRecord/Base.html#class-ActiveRecord::Base-label-Single+table+inheritance).
		-   `(association_name)_type` \- Stores the type for [polymorphic associations](https://guides.rubyonrails.org/association_basics.html#polymorphic-associations).
		-   `(table_name)_count` \- Used to cache the number of belonging objects on associations. For example, a `comments_count` column in an `Article` class that has many instances of `Comment` will cache the number of existent comments for each article.


[^1]: the Odin Project - Active Record Basics (https://www.theodinproject.com/courses/ruby-on-rails/lessons/active-record-basics-ruby-on-rails)

[^2]: Active Records Basics on Ruby on Rails Guide: https://guides.rubyonrails.org/active_record_basics.html