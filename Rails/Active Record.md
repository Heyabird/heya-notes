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