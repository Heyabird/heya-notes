# Active Record[^1]
- the interface that Rails gives you between the database and your application. It lets you structure your data models in a logical and nearly plain-English way.
- Rails is actually seven Ruby gems that work harmoniously together. Active Record is, to put it inelegantly, the gem that takes care of all the database stuff. It’s known as an “ORM”. 
- **Object Relational Mapping** (ORM) lets you interact with SQL data (or any other data, as long as config/database.yml is gucci) as if they were Ruby objects.
<hr>
#### Rails Models
- To store info about users, you create a database table called users. Then, you create a Rails model called User, which is just a Ruby file that inherits from Active Records  thus gets to use all the handy methods I was alluding to earlier like `all` and `find` and `create`.
- After creating the db by `$ rails db:create`, you can make the model by `$ rails generate model YourModelNameHere`.
	- This does two things: 
	1.  **create model** - create a model file in `app/models` which is set up like you just learned above.
	2.  **migrate** - create a database table called “users” that has the appropriate columns. This is done using a migration file and then running the migration.
		- migration = a script that tells Rails how you want to set up or change a database.
		- If you want to just do this step to modify rather than create new db, run `$ rails generate migration NameYourMigration`.
		- To revert migration you can just run `$ rails db:rollback`, edit the script file, and remigrate.

<hr>
#### ORM
To create a new user:

```bash
u = User.new(name: "Sven", email: "sven@theodinproject.com")
u.save
```
is the same thing as

```bash
u = User.create(name: "Sven", email: "sven@theodinproject.com")
```


[^1]: the Odin Project - Active Record Basics (https://www.theodinproject.com/courses/ruby-on-rails/lessons/active-record-basics-ruby-on-rails)


<hr>
#### Basic Validations

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

<hr>
#### Basic Associations

- **one-to-many**: “has many / belongs to” association (a User `has_many` Post objects associated with it and a Post `belongs_to` a single User).
	- A book belongs person A. Or a book belongs to multiple people.
- **many-to-many**: "has and belongs to many" association.
	- A dog has favorite humans A and B. A human has favorite dogs Y and Z.
	- To keep track of all the relationships, tt actually requires you to create another table (a join table, or “through” table).