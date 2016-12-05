# 2. Rails with Active Record and Action Pack


## 2.1 Introduction to Active Record


### 2.1.1 Github Repository for Module 1


* Each module in the course has a Github repository associated with it. The repository for Module 1 is located [here](https://github.com/jhu-ep-coursera/fullstack-course2-module1-fancy_cars).


* You can find PDFs of the Module 1 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course2-module1-fancy_cars/tree/master/Lectures).


* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course2-module1-fancy_cars/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 2.1.2 Recommended Books


#### Ruby on Rails framework


| Title | Author | Description |
| --- | --- | --- |
| Agile Web Development with Rails 4 | Dave Thomas, Sam Ruby and David Heinemeier Hansson | Great book on Rails! First runs through a Rails application and only then explains the topics, but a lot of people actually like that. |
| Ruby on Rails Tutorial | Michael Hartl | Does a wonderful job of explaining Rails development. |
| Rails 4 in Action | Ryan Bigg, Yehuda Katz, Steve Klabnik, Rebecca Skinner | Excellent book about Rails 4. |


#### Ruby language


| Title | Author | Description |
| --- | --- | --- |
| Eloquent Ruby | Russ Olsen | This book eloquently describes the Ruby programming language and does not put you to sleep in the process! Whether you are new to Ruby or have programmed in Ruby before, you will find “Eloquent Ruby” useful. |
| Programming Ruby | Dave Thomas, Andy Hunt, and Chad Fowler | The famous “Pickaxe” book, called so because of the pickaxe appearing on the cover. Complete Ruby reference. |
| Beginning Ruby | Peter Cooper | Excellent coverage for many Ruby topics. |
| Head First Ruby | Jay McGavren | This book just recently came out and everyone is talking about it! I am personally a huge fan of the Head First series - they explain stuff well and get you excited about learning in the process, so you don't fall asleep. |
| Learn To Program | Chris Pine | Great for Ruby beginners. Nice build up that won't overwhelm you. Some great examples of using Ruby in everyday life. |
| Ruby Cookbook | Lucas Carlson, Leonard Richardson | Lets you break your learning of Ruby down into chunks \(recipes\). |
| The Well-Grounded Rubyist | David A. Black | David Black knows his Ruby cold and is great at explaining it to others. The book has great reviews on Amazon. |
| Metaprogramming Ruby | Paolo Perrotta | A book about the cool “don’t-try-this-at-home” Ruby features. :\) |
































### 2.1.3 Scaffolding


* Console command

  ```
  $ cd [project folder]
  $ rails g scaffold car make color year:integer
  ```

  * car: Resource \(model\)
  * make, color, year: column names
  * integer: type
  * Default type: String



* This command will generate

  * Model
  * Controller with actions
  * Views
  * DB migration
  * Routes
  * test\_unit
  * can use --no-migration flag to disable migration generation



* Apply scaffolding to DB

  ```
  $ rake db:migrate
  ```



### 2.1.4 Database setup and SQLite


* Rails uses SQLite for database by default

* config\/database.yml

  * says where the database file located

    ```
    development:
    <<:*defualt
    database: db/development.sqlite3
    ```


* Database console

  ```
  $ rails db
  ```


* Help

  ```
  sqlite> .help
  ```


* table

  ```
  sqlite> .tables
  ```


* turn on headers and use column mode

  ```
  sqlite> .headers on
  sqlite> .mode columns
  ```


* SQL

  ```
  sqlite> select * from cars;
  ```


* exit

  ```
  sqlite> .exit
  ```


### 2.1.5 Introduction to Migration

* [Rails Guide](http://guides.rubyonrails.org/migrations.html)
* Ruby classes that extend
  * ActiveRecord::Migration


* **create\_table** and **drop\_table** create and drop the table
* db\/migrate\/yyyymmddxxxxx\_create\_cars.rb

  ```
  class CreateCars < ActiveRecord::Migration
    def change
      create_table :cars do |t|
        t.string :make
        t.string :color
        t.integer :year

        t.timestamps null: false
      end
    end
  end
  ```

  * Change method, Rails will guess what to do for undo rollback
  * up \/ down methods
  * null: true or false
  * limit: size
  * default: value
  * precision: value
  * scale: value


* Actual Type Mapping

  * :binary
  * :boolean
  * :decimal
  * :float
  * :integer
  * :string
  * :text
  * :time
  * :date
  * :datetime


* add\_column

  * source code

    ```
    add_column :table_name, :column_name, :column_type
    ```

  * command

    ```
    $ rails g migration add_price_to_cars 'price:decimal{10,2}'
    ```

  * migration file generated

    ```
    class AddPriceToCars < ActiveRecord::Migration
        def change
            add_column :cars, :price, :decimal, precision: 10, scale: 2
        end
    end
    ```


* remove\_column

  ```
  remove_column :table_name, :column_name
  ```


* rename\_column

  * source code

    ```
    rename_column :table_name, :old_column_name, :new_column_name
    ```

  * rails command

    ```
    $ rails g migration rename_make_to_company 'price:decimal{10,2}'
    ```


* migration file generated

  ```
  class RenameMakeToCompany < ActiveRecord::Migration
    def change
      rename_column :cars, :make, :company
    end
  end
  ```


* migrate

  ```
  $ rake db:migrate
  ```

  * this command will execute all migration in the db\/migrate folder


* rollback

  * undo the **last** migration

    ```
    $ rake db:rollback
    ```


* schema\_migrations table

* db\/schema.rb

  * the snapshot of your latest database
  * command to apply the schema to a new environment

    ```
    $ rake db:schema:load
    ```


### 2.1.6 Creating and Modifying Tables and Columns

* An **id** column is automatically created to be used as **primary key**

* **timestamps** method creates **created\_at** and **updated\_at** columns

* table schema

  ```
  sqlite> .schema cars
  ```


### 2.1.7 Dynamic Dispatch

* **static** vs. **dynamic** languages

  * advantage and disadvantage

* Example

  * A **Store** class
  * description and price of store products
  * To build a **reporting system** that **generate reports** for **different items** in the store
  * store class

  ```
  class store
    def get_piano_desc
      "Excellent piano"
    end
    def get_piano_price
      120.00
    end
    def get_violin_desc
      "Fantastic violin"
    end
    def get_violin_price
      110.00
    end
    # ... many other similar methods
  end
  ```

  * reporting system class

  ```
  require_relative 'store'
  class ReportingSystem
    def initialize
      @store = Store.new
    end
    def get_piano_desc
      @store.get_piano_desc
    end
    def get_piano_price
      @store.get_piano_price
    end
    # ... many other similar method
  end
  ```

  * _result_

  ```
  $ irb
  >
  > rs = ReportingSystem.new
  > puts "#{rs.get_piano_desc} costs #{rs.get_piano_price.to_s.ljust(6, '0') }"
  => Excellent piano costs 120.00
  ```

* **call** methods
  * using **dotnotation**: obj.method
  * **another way**: **send** method
  * first parameter is the **method name/symbol**; the rest are the **method arguments**


* Example

  * code

  ```
  class Dog
    def bark
      puts "Woof, woof!"
    end
    def greet(greeting)
      puts greeting
    end
  end
  ```

  * _result_

  ```
  $ irb
  > 
  > dog = Dog.new
  > dog.bark # => Woof, woof!
  > dog.send("bark") # => Woof, woof!
  > dog.send(:bark) # => Woof, woof!
  > method_name = :bark
  > dog.send method_name # => Woof, woof!
  > dog.send(:greet, "hello") # => hello
  ```

* Dynamic Dispatch - Advantage

  * Can decide **at runtime** which methods to call

  
* Example

  ```
  $ irb
  >
  > props = { name: "John", age: 15 }
  >
  > class Person; attr_accessor :name, :age; end
  >
  > person = Person.new
  > 
  > props.each { |key, value| person.send("#{key}=", value) }
  > person
  => #<Person:0xxxxxxxx @name="John", @age=15>
  ```


### 2.1.8 Dynamic Methods

* Not only can you **call** methods dynamically (with **send**) - you can also **define** methods dynamically

* *define_method :method_name** and a **block** which contains the **method definition**

* Defines an **instance method** for the class

* Example 1

  ```
  class Whatever
    define method :make_it_up do
      puts "Whatever..."
    end
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > whatever = Whatever.new
  > whatever.make_it_up # => Whatever...
  ```

* Example previous

  ```
  require_relative 'store'
  class ReportingSystem
    def initialize
      @store = Store.new
    end
    def get_piano_desc
      @store.get_piano_price
    end
    def get_piano_price
      @store.get_piano_price
    end
    # ...many more similar methods
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > rs = ReportingSystem.new
  > puts "#{rs.get_piano_desc} costs #{rs.get_piano_price.to_s.ljust(6, '0') }"
  => Excellent piano costs 120.00
  ```

* Using Dynamic Method

  ```
  require_relative 'store'
  class ReportingSystem
    def initialize
      @store = Store.new
      @store.methods.grep(/^get_(.*)_desc/) { ReportingSystem.define_report_methods_for $1 }
    end
    def self.define_report_methods_for (item)
      define_method("get_#{item}_desc") { @store.send("get_#{item}_desc") }
      define_method("get_#{item}_price") { @store.send("get_#{item}_price") }
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > rs = ReportingSystem.new
  > puts "#{rs.get_piano_desc} costs #{rs.get_piano_price.to_s.ljust(6, '0') }"
  => Excellent piano costs 120.00
  ```

  * **/^get_(.*)_desc/** extracts product name, and set the value to **$1**


* Improved Reporting System

  * No more duplication: not need to write all of these **repetitive methods**
  * If someone adds a **new item** to the **Store** class, the **ReportingSystem** class already **knows about it**


### 2.1.9 Ghost Methods

* If a method is **invoked** and it's **NOT FOUND**, was it really called at all?

  * _demo_

  ```
  $ irb
  > 
  > class SomeClass; end
  => nil
  > some_class = SomeClass.new
  => #<SomeClass: 0x????????>
  > some_class.i_dont_exist
  NoMethodError: undefined method 'i_dont_exist' for #<SomeClass: 0x??????>
  ```


* **method_missing** ... method

  * Ruby looks for the method **invoked** in the class to which it belongs
  * Then it goes up the **ancestors tree** \(classes and modules\)
  * If it still doesn't find the method, it calls **method\_missing** method
  * The default **method\_missing** implementation throws **NoMethodError**


* **Overriding** method\_missing

  * Since **method\_missing** is just a method, you can easily **override** it
  * You have access to

    * **Name** of the method called
    * Any **arguments** passed in
    * A **block** if it was passed in


* Example

  * _code_

  ```
  class Mystery
    # no_methods defined
    def method_missing (method, *args)
      puts "Looking for ..."
      puts "\"#{method}\" with params (#{args.join(',')}) ?"
      puts "Sorry... He is on vacation..."
      yield "Ended up in method_missing" if block_given?
    end
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > m = Mystery.new
  > m.solve_mystery("abc", 123123) do |answer|
      puts "And the answer is: #{answer}"
    end
  >
  # => Looking for ...
  # => "solve_mystery" with params (abc.123123) ?
  # => Sorry... He is on vacation..
  # => And the answer is: Ended up in method_missing
  ```


* Ghost Methods

  * **method_missing** gives you the power to **fake** the methods
  * Call **ghost methods** because the methods **don't exist**
  * Ruby's build-in classes use **method_missing** and dynamic methods all over the plac...


* Struct and OpenStruct

  * Struct

    * Generator of **specific classes, each one of which is defined to **hold** a set of variables and their accessors ("Dynamic Methods")

  * OpenStruct

    * Object (similar to **struct**) whose **attributes** are created dynamically when **first assigned** ("Ghost methods")

  * Example

  ```
  Customer = Struct.new(:name, :address) do
    def to_s
      "#{name} lives at #{address}"
    end
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > jim = Customer.new("Jim", "-1000 Wall Street")
  > puts jim # => Jim lives at -1000 Wall Street
  >
  > require 'ostruct' # => need to require ostruct for OpenStruct
  > 
  > some_obj = OpenStruct.new(name: "Joe", age: 15)
  > some_obj.sure = "three"
  > some_obj.really = "yes, it is true"
  > some_obj.not_only_strings = 10
  > puts "#{some_obj.name} #{some_obj.age} #{some_obj.really}"
  => Joe 15 yes, it is true
  ```


* So, now, the ReportingSystem

  * _code_

  ```
  require_relative 'store'
  class ReportingSystem
    def initialize
      @store = Store.new
    end
    def method_missing(name, *args)
      super unless @store.respond_to?(name)
      @store.send(name)
    end
  end
  ```

  * _demo_

  ```
  $ irb
  >
  > rs = ReportingSystem.new
  > puts "#{rs.get_piano_desc} costs #{rs.get_piano_price.to_s.ljust(6, '0') }"
  => Excellent piano costs 120.00
  ```


* method\_missing and performance issue

  * Since the **invocation** is **indirect**, could be a little slower
  * Most of the time, it will probably not matter too much
  * If it does, you can consider a hybrid approach
    * Define a **real method** from inside **method\_missing** after an attempted "call"


### 2.1.10 Introduction to Active Record

* ORM - Object-Relational Mapping

* It is Rails default ORM

* 3 prerequisites

  * ActiveRecord has to know **where to find your database**

    * when Rails is loaded, this info is read from **config\/database.yml** file
    * table name is a plural name, class name is singular name
    * table has primary key, named as id

  * Rails console

    ```
    $ rails c
    > exit
    ```

    * can interact with the model class methods

    ```
    > Car.column_names
    > Car.primary_key
    ```


* Model generator

  ```
  $ rails g model person first_name last_name
  ```

  * will generate model, migration and unit test
  * need execute migration

  ```
  $ rake db:migrate
  ```


* config\/initializers\/inflections.rb

* reload! to refresh and update in source code

  ```
  > reload!
  ```


### 2.1.11 Active Record CRUD

* CRUD - create, retrive, update, delete


#### 2.1.11.1 create

* new

  ```
  > p1 = Person.new; p1.first_name = "Joe"; p1.last_name = "Smith"
  > p1.save
  ```

* hash

  ```
  > p2 = Person.new(first_name: "Joe", last_name: "Smith")
  > p2.save
  ```

* create

  ```
  > p3 = Person.create(first_name: "Joe", last_name: "Smith")
  ```


#### 2.1.11.2 Retrive

* find\(id\) or find\(id1, id2\)

  * throws a RecordNotFound exception if not found

* find\_by

  * will not throw exception

* find\_by!

  * will throw exception

* first, last, take, all

* order\(:column\) or order\(column: :desc\)

* pluck

* where\(hash\)

* limit\(n\)

* offset\(n\)

* rails console

  ```
  > Person.all.order(first_name: :desc)
  > Person.all.order(first_name: :desc).to_a
  > Person.fist
  > Person.last
  > Person.all[0]
  > Person.take
  > Person.take 2
  > Person.all.map {|person| person.first_name}
  > Person.pluck(:first_name)
  > Person.where(last_name: "Doe")
  > Person.where(last_name: "Doe").first
  > Person.where(last_name: "Doe")[0]
  > Person.where(last_name: "Doe").pluck(:first_name)
  > Person.find_by(last_name: "Doe")
  > Person.find_by(last_name: "Wei")
  > Person.find_by!(last_name: "Wei")
  ```


#### 2.1.11.3 Update

* retrive, modify, save
* update with **hash**
* update\_all for batch updates
* rails console

  ```
  > jane = Person.find_by first_name: "Jane"
  > jane.last_name = "Smith"
  > jane.save
  >
  > Person.find(3)
  >
  > jane = Person.find_by(last_name: "Smith").update(last_name: "Smithon")
  > 
  ```


#### 2.1.11.4 Delete

* destroy\(id\) or destroy

  * Removes a particular instance from the DB
  * **Instantiates** an object first and **performs callbacks** before removing the record
  * see [Rails Guide](http://guides.rubyonrails.org/active_record_callbacks.html)


* delete\(id\)

  * Removes the row from DB directly


* delete\_all
  * be **CAREFUL**


* rails console

  ```
  > Person.count
  >
  > jane = Person.find_by first_name: "Jane"
  > jane.destroy
  >
  > joe = Person.find_by first_name: "Joe"
  > Person.delete(joe.id)
  ```


## 2.2 Deep Dive into Active Record


### 2.2.1 Github Repository for Module 2

* Each module in the course has a Github repository associated with it. The repository for Module 2 is located [here](https://github.com/jhu-ep-coursera/fullstack-course2-module2-advanced-ar).

* You can find PDFs of the Module 2 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course2-module2-advanced-ar/tree/master/Lectures).

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course2-module2-advanced-ar/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 2.2.2 Seeding the Database

* create Rails app

  ```
  $ rails new advanced_ar
  $ cd advanced_ar
  ```


* create model

  ```
  $ rails g model person first_name age:integer last_name
  ```


* migrate

  ```
  $ rake db:migrate
  ```


* rake db:seed

  ```
  $ rake --describe db:seed
  ```

* db\/seeds.rb

  ```
  Person.destroy_all
  Person.create! [
  {first_name: "Kalman", last_name: "Smith", age: 33},
  {first_name: "John", last_name: "Smith", age: 34},
  {first_name: "Kalman", last_name: "Gates", age: 43}
  ]
  ```

  * Use create! here to stop the process with exception if anything wrong


* rake db:seed

  ```
  $ rake db:seed
  ```


* check DB

  ```
  $ rails db
  sqlite>
  sqlite> .headers on
  sqlite> .mode columns
  sqlite> select * from people;
  ```


### 2.2.3 SQL Fragments and Dangers of SQL Injection

* Exact Searches

  * find\(id\) or find\(id1, id2\)
  * find\_by\(hash\)
  * where\(hash\)


* Including SQL fragment

  * Specify SQL fragment \(as opposed to hash\) inside the **where** and **find\_by**
  * Very powerful, but possible for **SQL injection**

  ```
  > Person.where("age BETWEEN 30 and 40").to_a
  > Perosn.find_by("first_name LIKE '%man'")
  ```


* What is SQL Injection


### 2.2.4 Array and Hash Condition Syntax

* Array Condition Syntax

  * Specify SQL fragment with ?
  * Automagically **performs** conversions on the input values and **escapes** strings in the SQL
  * Immune to SQL injection
  * Similar to a PreparedStatement in Java

  ```
  > Person.where("age BETWEEN ? AND ?", 28, 34).to_a
  > Person.where("first_name LIKE ? OR last_name LIKE ?", '%J%', '%J%').to_a
  > 
  ```


* Hash Condition Syntax

  ```
  > Person.where("age BETWEEN :min_age AND :max_age", min_age: 22, max_age: 32).to_a
  > Person.where("first_name LIKE :pattern OR last_name LIKE :pattern", pattern: '%J').to_a
  ```


### 2.2.5 Association

#### 2.2.5.1 One-to-One Association

* Convention

  * Default name for the foreign key is {master\_table\_singular}\_id, e.g. person\_id


* Example: one person has one person\_info

  ```
  $ rails g model personal_info height:float weight:float person:references
  ```

  * xxxxxx\_create\_personal\_infos.rb

  ```
  class CreatePersonalInfos < ActiveRecord::Migration
    def change
      create_table :personal_infos do |t|
        t.float :height
        t.float :weight
        t.references :person, index: true, foreign_key: true
        t.timestamps null: false
      end
    end
  end
  ```


* rake db:migrate

  ```
  $ rake db:migrate
  ```


* check db schema

  ```
  $ rails db
  sqlite> .schema personal_infos
  ```


* One-to-One Association

  ```
  > bill = Person.find_by first_name: "Bill"
  > bill.personal_info
  > pil = Personal_info.create height: 6.5, weight: 22
  > bill.personal_info = pil
  ```


* New methods are ready for Person model

  * build\_personal\_info\(hash\)
  * create\_personal\_info\(hash\)
  * **Both** methods will remove the previous reference in the DB
  * **create\_xxx** method will create a record in DB right away, but **build\_xxx** will not 


* source code

  ```
  has_one
  ```

  * _and_

  ```
  belongs_to
  ```


#### 2.2.5.2 One-to-Many Association

* Convention

  * Default name for the foreign key is {master\_table\_singular}\_id, e.g. person\_id


* Example: one person has many jobs

  ```
  $ rails g model job title company position_id person:references
  ```

  * xxxxxx\_create\_jobs.rb

    ```
    class CreateJobs < ActiveRecord::Migration
      def change
        create_table :jobs do |t|
          t.string :title
          t.string :company
          t.string :position_id
          t.reference :person, index: true, foreign_key: true

          t.timestamps null: false
        end
      end
    end
    ```


* source code

  * person.rb

    ```
    class Person < ActiveRecord::Base
      has_one :personal_info
      has_many :jobs
    end
    ```

  * job.rb

    ```
    class Job < ActiveRecord::Base
      belongs_to :person
    end
    ```


* rake db:migrate

  ```
  $ rake db:migrate
  ```


* check db schema

  ```
  $ rails db
  sqlite> .schema jobs
  ```


* One-to-Many Association

  ```
  $ rails c
  >
  > ActiveRecord::Base.logger = nil
  >
  > Job.create company: "MS", title: "Dev", position_id: "1234"
  > p1 = Person.first
  > p1.jobs
  >
  > p1.jobs << Job.first
  > Job.first.person
  ```

  * ActiveRecord::Base.logger = nil will **disable** the logger


* More Methods

  * person.jobs = jobs
    * Replaces existing jobs with a new array

  * person.jobs &lt;&lt; job\(s\)
    * Append the jobs

  * person.jobs.clear
    * Disassociates the relationship


* seeds.rb

  ```
  Person.destroy_all
  Person.create! [
  ...
  ]

  Person.first.jobs.create! [
    { title: "Dev", company: "MS", position_id: "#1234" },
    { title: "Dev", company: "MS", position_id: "#1254" }
  ]

  Person.last.jobs.create! [
    { title: "Sr. Dev", company: "MS", position_id: "#2234" },
    { title: "Sr. Dev", company: "MS", position_id: "#2254" }
  ]
  ```


* rake db:seed

  ```
  $ rake db:seed
  ```


* build

  * You can use 'build' instead of 'create', but 'build' will not automatically save to DB


* where

  ```
  $ rails c
  >
  > ActiveRecord::Base.logger = nil
  > 
  > Person.first.jobs.where(company: "MS").count
  > Person.last.jobs.where(company: "MS").count
  > Person.first.jobs.where(company: "MS").to_a
  ```


* Options for has\_many

  ```
  class Person < ActiveRecord::Base
    has_one :personal_info
    has_many :jobs
    has_many :my_jobs, class_name: "Job"
  end
  ```

  * class\_name is the model class name

  ```
  $ rails c
  >
  > Person.first.my_jobs
  ```


* :dependent

  * **has\_many**, **has\_one** and **belongs\_to** support **:dependent** option which lets you specify the fate of the association when the parent gets destroyed.
  * :delete
  * :destroy
  * :nullify


* Example

  * source code

    ```
    class Person < ActiveRecord::Base
      has_one :personal_info, dependent: :destroy
      has_many :jobs
      has_many :my_jobs, class_name: "Job"
    end
    ```

  * rails console

    ```
    > mike = Person.find_by first_name: "Michael"
    > id = mike.personal_info.id
    > mike.destroy
    > Personal_info.find id
    ```


#### 2.2.5.3 Many-to-Many Association

* People and hobbies

* has\_and\_belongs\_to\_many

* Need to create an extra table without a model

* Convention

  * Plural model names separated by an underscore in **alphabetical** order


* Hobbies and Hobbies\_People

  ```
  $ rails g model hobby name
  $ rails g migration create_hobbies_people person:references hobby:references
  $ rake db:migrate
  ```


* xxxx\_create\_hobbies\_people.rb

  ```
  class CreateHobbiesPeople < ActiveRecord::Migration
    def change
      create_table :hobbies_people, id: false do |t|
        t.references :person, index: true, foreign_key: true
        t.references :hobby, index: true, foreign_key: true
      end
    end
  end
  ```

  * Since this is a join table, it is no need for primary key: **id: false**


* schema

  ```
  $ rails db
  sqlite>
  sqlite> .schema %hobbies%
  ```


* person.rb

  ```
  class Person < ActiveRecord::Base
    has_one :personal_info, dependent: :destroy
    has_many :jobs
    has_many :my_jobs, class_name: "Job"
    has_and_belongs_to_many :hobbies
  end
  ```


* hobby.rb

  ```
  class Hobby < ActiveRecord::Base
    has_and_belongs_to_many :people
  end
  ```

* rails console

  ```
  > josh = Person.find_by first_name: "Josh"
  > lebron = Person.find_by first_name: "LeBron"
  > programming = Hobby.create name: "Programming"
  > josh.hobbies << programming; leborn.hobbies << programming
  > programming.people
  ```

* Summary

  * Many\_to\_Many contains 2 models and 3 migrations
  * Join table needs to only exist in DB, but not in Ruby code


### 2.2.5.4 Rich Many\_to\_Many Association

* May need to **keep some more data** in the join table
* May nned to store **grandchild** relationships on a model, like user -&gt; articles -&gt; comments
* ActiveRecord provides a :through option for this purpose
* **Basic idea**:
  * 1st. create a regular parent-child relationship
  * 2nd. use the child model as a **join** between the parent and grandchild


* Person, Jobs, Salary\_Range

  ```
  $ rails g model salary_range min_salary:float max_salary:float job:references
  $ rake db:migrate
  ```


* xxxxxx\_create\_salary\_ranges.rb

  ```
  class CreateSalary_Ranges < ActiveRecord::Migration
    def change
      create_table :salary_ranges do |t|
        t.float :min_salary
        t.float :max_salary
        t.references :job, index: true, foreign_key: true
        t.timestamps null: flase
      end
    end
  end
  ```


* job.rb

  ```
  class Job < ActiveRecord::Base
    belongs_to :person
    has_one :salary_range
  end
  ```


* salary\_range.rb

  ```
  class SalaryRange < ActiveRecord::Base
    belongs_to :job
  end
  ```


* person.rb
  ```
  class Person < ActiveRecord::Base
    has_one :personal_info, dependent: :destroy
    has_many :my_jobs, class_name: "Job"
    has_many_and_belongs_to_many :hobbies
    has_many :jobs
    has_mamy :approx_salaries, through: :jobs, source: :salary_range
  end
  ```


* rails console

  ```
  > lebron = Person.find_by(first_name: "LeBron")
  > lebron.jobs.count
  => 2
  >
  > lebron.jobs.pluck(:id)
  => [12, 13]
  >
  > Job.find(12).create_salary_range(min_salary: 1000.00, max_salary: 2000.00)
  > Job.find(12).create_salary_range(min_salary: 1000.00, max_salary: 2000.00)
  > lebron.approx_salaries
  ```


* More than through: **Calculations**

  ```
  has_one :personal_info, dependent: :destroy
  has_many :my_jobs, class_name: "Job"
  has_many_and_belongs_to_many :hobbies
  has_many :jobs
  has_mamy :approx_salaries, through: :jobs, source: :salary_range

  def max_salary
    approx_salaries.maximum(:max_salary)
  end
  ```

  * method based on **approx\_salary** 
  * NOT ONLY maximum, average, minimum and sum are also available
  * [guide](http://api.rubyonrails.org/classes/ActiveRecord/Calculations.html)


* rails console

  ```
  > lebron = Person.find_by last_name: "James"
  > lebron.max_salary
  ```


### 2.2.6 Active Record Scopes

* Default Scope

  * Example, to do

    ```
    > Hobby.pluck :name
    => ["Programming", "Music"]
    ```

  * Solution with default\_scope

    ```
    class Hobby < ActiveRecord::Base
      has_and_belongs_to_many :people
      default_scope { order :name }
    end
    ```

  * Result

    ```
    > Hobby.pluck :name
    => ["Music", "Programming"]
    >
    > Hobby.unscoped.pluck :name
    => ["Programming", "Music"]
    ```


* Named scope

  * scope :name, lambda

    ```
    class Person < ActiveRecord::Base
      has_one :personal_info, dependent: :destroy
      has_many :my_jobs, class_name: "Job"
      has_many_and_belongs_to_many :hobbies
      has_many :jobs
      has_mamy :approx_salaries, through: :jobs, source: :salary_range

      def max_salary
        approx_salaries
      end

      scope :ordered_by_age, -> { order age: :desc }
      scope :starts_with, -> (starting_string){ where("first_name LIKE ?", "#{starting_string}%")}
    end
    ```

  * rails console

    ```
    > Person.ordered_by_age.pluck :age
    => [75, 57, 33, 30, 27, 27]
    > 
    > Person.ordered_by_age.starts_with("Jo").pluck :age, :first_name
    => [[57, "Josh"], [27, "John"], [27, "John"]]
    >
    > Person.ordered_by_age.limit(2).starts_with("Jo").pluck :age, :first_name
    ```


* Scopes always return **ActiveRecord::Relation**


### 2.2.7 Validations

* Validations
  * Validation is to control what goes to DB
  * Not every input might be appropriate
  * If validations fail - the information should not be saved to DB


* presence: true
  * Make sure the field contains **some data**


* uniqueness: true
  * Make sure no record exists in the DB already with the **given value** for the specified attribute


* :numericality
  * validates numeric input


* :length
  * validates value is a certain length


* :format
  * validates value complies with some regular **expression format**


* :inclusion
  * validates value is inside **specified range**


* :exclusion
  * validates value is out of the **specified range**


* Writing your own validation
  * wrtie a method to do some validations and calls errors.add\(columnname, error\) when it encounters an error condition
  * Specifiy the method as a symbol for the validate method


* Example

  ```
  class SalaryRange < ActiveRecord::Base
    belongs_to :job
    validate :min_is_less_than_max

    def min_is_less_than_max
        if min_salary > max_salary
            errors.add(:min_salary, "cannot be greater than maximum salary!")
        end
    end
  end
  ```

  * :numericality build-in validator can do the same thing in this example. Here is just to demo **Own Validation**


* rails console

  ```
  > sr = SalaryRange.create min_salary: 300.00, max_salary: 100.00
  > sr.errors
  > sr.errors.full_message
  ```


* job.rb

  ```
  class Job < ActiveRecord::Base
    belongs_to :person
    has_one :salary_range

    validates :title, :company, presendce: true
  end
  ```


* rails console

  ```
  > job = Job.new
  > job.errors
  >
  > job.save
  > job.errors
  > job.errors.full_message
  ```

  * error happens when you save to DB


* guide
  * [http:\/\/guides.rubyonrails.org\/active\_record\_basics.html](http://guides.rubyonrails.org/active_record_basics.html)
  * [http:\/\/guides.rubyonrails.org\/active\_record\_querying.html](http://guides.rubyonrails.org/active_record_querying.html)
  * [http:\/\/guides.rubyonrails.org\/association\_basics.html](http://guides.rubyonrails.org/association_basics.html)
  * [http:\/\/guides.rubyonrails.org\/active\_record\_callbacks.html](http://guides.rubyonrails.org/active_record_callbacks.html)


### 2.2.8 N+1 Queries Issue and DB Transactions

#### 2.2.8.1 N+1 Queries

* query one record

  ```
  > Person.first.personal_info.weight
  ```

  * two SQL queries


* query many records

  ```
  > Person.all.each { |p| puts p.personal_info.weight }
  ```

  * 1 + N SQL queries


* use **include**

  ```
  > Person.include(:personal_info).all.each { |p| puts p.personal_info.weight }
  ```

  * **ONLY** two queries


#### 2.2.8.2 Transactions

* \[guide\]\([http:\/\/api.rubyonrails.org\/classes\/ActiveRecord\/Transactions\/ClassMethods.html](http://api.rubyonrails.org/classes/ActiveRecord/Transactions/ClassMethods.html)

* Example

  ```
  ActiveRecord::Base.transaction do
    david.withdrawal(100)
    mary.deposit(100)
  end
  ```


## 2.3 Introduction to Action Pack

### 2.3.1 Github Repository for Module 2

* Each module in the course has a Github repository associated with it. The repository for Module 3 is located [here](https://github.com/jhu-ep-coursera/fullstack-course2-module3-blogposts).

* You can find PDFs of the Module 3 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course2-module3-blogposts/tree/master/Lectures).

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course2-module3-blogposts/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 2.3.2 Introduction to Action Pack

* Action Pack
  * ActionController + ActionView = ActionPack


* Work flow
  * Request sent
  * Router routes request to controller
  * Controller interact with Model
  * Controller invokes View
  * View renders data


* new web app

  ```
  $ rails new my_log
  $ cd my_log
  $
  $ rails g scaffold post title content:text
  $
  $ rake db:migrate
  ```

  * Scaffolding creates
    * Migration
    * Model
    * **Routes**
    * **Restful Controller**
    * **Views**
    * More ...



* ActionView: ERB
  * HTML file with .erb extension 
  * ERB = **embed** Ruby into html
  * Two tags
    * &lt;% ... ruby code ... %&gt;
    * &lt;%= ... ruby code ... %&gt;



* ActionController
  * Ruby class containing **one or more** actions
  * Each action is responsible for **responding to a request** to perform some task
  * Unless otherwise stated - when an action is **finished firing**, it **renders a view**


* routes.rb

  ```
  Rails.application.routes.draw do
  resources :posts
  end
  ```

  * Convension Over Configuration: **resources :posts**


### 2.3.3 REST and Rails

* [REST](http://www.xfront.com/REST-Web-Services.html) = **Re**presentational **S**tate **T**ransfer

* REST is all about resources

  * **List** available resourcess
  * **Show** a specific resource
  * **Destroy** an existing resource
  * **Provide a way to create** a new resource
  * **Create** a new resource
  * **Provide a way to update** an existing resource
  * **Update** an existing resource


* Rails Convention

  * source code

    ```
    class PostController < ApplicationController

      # GET /posts
      def index

      # GET /posts/1
      def show

      # DELETE /posts/1
      def delete

      # GET /posts/new
      def new

      # GET /posts/1/edit
      def edit

      # POST /posts
      def create

      # PATCH/PUT /posts/1
      def update
    end
    ```

  * table

    | HTTP Method | Named Routes | Parameters | Controller Action | Purpose |
    | --- | --- | --- | --- | --- |
    | GET | posts\_path | - | index | List all |
    | GET | post\_path | ID | show | Show one |
    | GET | new\_post\_path | - | new | Provide form to input new post |
    | POST | posts\_path | Record hash | create | Create new record \(in DB\) |
    | GET | edit\_post\_path | ID | edit | Provide form to edit record |
    | PUT\/PATCH | post\_path | ID and Record hash | update | Update record \(in DB\) |
    | DELETE | post\_path | ID | destroy | Remove record |

  * rake routes

    ```
    $ rake routes
    ......Prefix     Verb       URI Pattern                  Controller#Action
    .......posts     GET        /posts(.:format)             posts#index
    .................POST       /posts(.:format)             posts#create
    ...new_posts     GET        /posts/new(.:format)         posts#new
    ..edit_posts     GET        /posts/:id/edit(.:format)    posts#edit
    .......posts     GET        /posts/:id(.:format)         posts#show
    .................PATCH      /posts/:id(.:format)         posts#update
    .................PUT        /posts/:id(.:format)         posts#update
    .................DELETE     /posts/:id(.:format)         posts#destroy
    ```



### 2.3.4 Restful Actions

#### 2.3.4.1 Index

* Controller source code

  ```
  class PostsController < ApplicationController

  # GET /posts
  # GET /posts.json
  def index
    @posts = Post.all
  end
  end
  ```


* View source code

  ```
  <tbody>
  <% @posts.each do |post| %>
    <tr>
      <td><%= post.title %></td>
      <td><%= post.content %></td>
      <td><%= link_to 'Show', post %></td>
      <td><%= link_to 'Edit', edit_post_path(post) %></td>
      <td><%= link_to 'Destroy', post, method: :delete, data: { confirm: 'Are you sure?' }  %></td>
    </tr>
  <% end %>
  </tbody>
  ```

  * post = post\_path\(post\)


* index.json.jbuilder

  ```
  json.array!(@posts) do |post|
  json.extract! post, :id, :title, :content
  json.url post_url(post, format: :json)
  end
  ```

  * [jbuilder](https://github.com/rails/jbuilder)


#### 2.3.4.2 Show

* Controller source code

  ```
  class PostsController < ApplicationController
    before_action :set_post, only: [:show, :edit, :update, :destroy]

    # GET /posts/1
    # GET /posts/1.json
    def show
    end

    private
      def set_post
        @post = Post.find(params[:id])
      end
  end
  ```

  * Sometimes makes sense to group multiple actions that execute the same code. We use **before\_action** here


* View source code

  ```
  <p id="notice"><%= notice %><p>

  <p>
    <strong>Title:</strong>
    <%= @post.title %>
  </p>

  <p>
    <strong>Content:</strong>
    <%= @post.content %>
  </p>

  <%= link_to 'Edit', edit_post_path(post) %>
  <%= link_to 'Back', posts_path %>
  ```

  * post = post\_path\(post\)


* show.json.jbuilder

  ```
  json.extract! @post, :id, :title, :content, :create_at, :updated_at
  ```


#### 2.3.4.3 Destroy

* helper functions
  * respond_to
    * Specify how to respond to a request based on a request format
    * Takes an **optional block** where the argument is the format
    * Block specifies **how to handle** each format
      * format.format_name - matching template
      * format.format_name { do_something_other_than_just_displaying_the_matching_template }

    * redirect_to
      * Instead of rendering a template - **send a response** to the browser: "Go here!"
      * usually **takes a (full) URL as a parameter
      * could either be a regular URL (like http://google.com) or a **named route**
      * If the parameter is an object - Rails will attempt to **generate a URL** for that object


* Controller source code

  ```
  class PostsController < ApplicationController
    before_action :set_post, only: [:show, :edit, :update, :destroy]

    # DELETE /posts/1
    # DELETE /posts/1.json
    def destroy
      @post.destroy
      respond_to do |format|
        format.html { redirect_to posts_url, notice: 'Post was successfully destroyed.' }
        format.json { head :no_content }
    end

    private
      # Use callbacks to share common setup or constraints between actions
      def set_post
        @post = Post.find(params[:id])
      end
  end
  ```

    * Why redirect?
      * Redirect is an action of sending back to the browser, to ask the browser to fetch another web page or take another controller action.
      * For 'delete' action, nothing to show, so redirect


#### 2.3.4.4 New

* controller source code

  ```
  class PostsController < ApplicationController
    # GET /posts/new
    def new
      @post = Post.new
    end
  end
  ```

* new.html.rb

  ```
  <h1>New Post</h1>
  <%= render 'form' %>
  <%= link_to 'Back', posts_path %>
  ```
  
  * render is Partial


#### 2.3.4.5 Create

* Create a ** New Post Object** with parameters that were **passed** from the new form

* Try to **save** the object to the DB

* If successful, **redirect** to **show** template

* If unsuccessful, **render new** action again

* Controller source code

  ```
  class PostsController < ApplicationController

    # POST /posts
    # POST /posts.json
    def create
      @post = Post.new(post_params)

      respond_to do |format|
        if @post.save
          format.html { redirect_to @post, notice: 'Post was successfully created.' }
          format.json { render :show, status: :created, location: @post }
        else
          format.html { render :new }
          format.json { render json: @post.errors, status: :unprocessable_entity }
        end
      end
    end

    private
    # Never trust parameters from the scary internet, only allow the white list through.
      def post_params
        params.require(:post).permit(:title, :content)
      end
  end
  ```

  * **ActiveModel::ForbiddentAtributesError** will happen if you never check input parameters
  * This is **2.3.4.2 Strong Parameters**


#### 2.3.4.6 Edit

* Similiar with the **new** action

* Retrive a post object based on the **_id_** provided (as part of the URI)

* \(Implicit\) Look for **edit.html.erb**

* Controller source code

  ```
  class PostsController < ApplicationController
    before_action :set_post, only: [:show, :edit, :update, :destroy]

    # GET /posts/1/edit
    def edit
    end

    private
      def set_post
        @post = Post.find(params[:id])
      end
  end
  ```


* edit.html.erb

  ```
  <h1>Editing Post</h1>

  <%= render 'form' %>

  <%= link_to 'Show', @post %> | 
  <%= link_to 'Back', posts_path %>
  ```

    * 'form' is a **Partial**



#### 2.3.4.7 Update

* **Retrive** an existing post using **_id_** parameter

* **Update** post object with **Strong Parameters** that were passed from the **edit** form

* Try to **save** the object to the DB

* If successful, **redirect** to **show** template

* If unsuccessful, **render** **edit** action template again


* Controller source code

  ```
  class PostsController < ApplicationController

    # PATCH/PUT /posts/1
    # PATCH/PUT /posts/1.json
    def update
      respond_to do |format|
        if @post.update(post_params)
          format.html { redirect_to @post, notice: 'Post was successfully updated.' }
          format.json { render :show, status: :ok, location: @post }
        else
          format.html { render :edit }
          format.json { render json: @post.errors, status: :unprocessable_entity }
        end
      end
    end

    private
      # Use callbacks to share common setup or constraints between actions
      def set_post
        @post = Post.find(params[:id])
      end

      # Never trust parameters from the scary internet, only allow the white list through.
      def post_params
        params.require(:post).permit(:title, :content)
      end
  end
  ```


### 2.3.5 Strong Parameters and Flash

#### 2.3.5.1 Strong Parameters

* [Strong Parameters](http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)

* We must check the white list before take the input parameters for **create** and **update** actions

* Source code in the create action

  ```
  def create
    @post = Post.new(post_params)
    ... ...
  end

  private
    # Never trust parameters from the scary internet, only allow the white list through.
    def post_params
      params.require(:post).permit(:title, :content)
    end
  ```


#### 2.3.5.2 Flash

* **Problem:** We want to **redirect** a user to a different page on our site, but at the same time **give** him some sort of a **message**.

* **Solution:** flash - a **hash** where the data you put in **persists** for exactly **ONE request AFTER** the current request.

* **Flash** persists for exactly one request after the current request/response cycle

* How to use **Flash**
  * Put your content into flash by doing

    ```
    flash[:attribute] = value
    ```
  * Two **common** attributes: **notice** (good) and **alert** (bad)
  * It is so common in fact, that the **redirect_to** takes a **:notice** or **:alert** keys


* Source code in the create action

  ```
  def create
    @post = Post.new(post_params)

    respond_to do |format|
      if @post.save
        format.html { redirect_to @post, notice: 'Post was successfully created.' }
      ...
  ```


### 2.3.6 Partials

* **application.html.erb** enables you to **maintain layout code** for the entire application in **one place**

* Partials are similar to regular templates, but they have a more **refined** set of capabilities.

* Named with **underscore** \(\_\) as the leading character

* Rendered with **render** 'particalname' (no underscore)

* **Render** also accepts a **second argument**, a hash of **local** variables used in the partial.

* Similar to passing local variables, you can also **render** a specific object.

  ```
  <%= render @post %>
  ```

  * will render a partial in **app/views/posts/_post.html.erb** and automatically assign a local variable **post**.
  * This is convention Over Configuration

* Rendering Conllection of Partials

  ```
  <%= render @posts %>
  ```

  * \_is equivalent to\_

  ```
  <% @posts.each do |post| %>
    <%= render post %>
  <% end %>
  ```

* \_form.html.erb - **display errors**

  ```
  <%= form_for(@post) do |f| %>
    <% if @car.errors.any? %>
      <div id="error_explanation">
        <h2><%= pluralize(@car.errors.count, "error") %> prohibited this car from being saved:</h2>
        <ul>
          <% @post.errors.full_messages.each do |message| %>
            <li><%= message %></li>
          <% end %>
        </ul>
      </div>
    <% end %>
    <div class="field">
      <%= f.label :title %><br>
      <%= f.text_field :title %>
    </div>
    <div class="field">
      <%= f.label :content %><br>
      <%= f.text_area :content %>
    </div>
    <div class="actions">
      <%= f.submit %>
    </div>
  <% end %>
  ```


* post.rb

  ```
  class Post < ActiveRecord::Base
    validates :title, presence: true
  end
  ```

  * http://localhost:3000/posts/1

  * If you leave Titel field empty and click update, you will get error message.



### 2.3.7 Form Helpers and Layouts

#### 2.3.7.1 Form Helpers

* \_form.html.erb

  ```
  <%= form_for(@post) do |f| %>
  ```

  * form_for with parameters, such as **post** in this case, that match up with model's attributes

  * If the object (@post here) has been persisted before, it would generate a form which will submit to an update action. Otherwise, it would generate a form which will submit to a create action instead.

  ```
  <div class="actions">
    <%= f.submit %>
  </div>
  ```

  * Submit button for submitting the form  

  * The text on the button is decided based on the persist attribute of the object (@post here), unless you define the text yourself.


* form\_for
  * Generate a **form tag** for passed in object
  * Unlike a regular HTML form, Rails uses **POST** by default.


* f.label
  * Outputs HTML label tag for the **provided attribute**
  * To **customize** label description, **pass in a string** as a second parameter.  

   ```
   <div class="field">
     <%= f.label :title, "Heading" %><br>
     <%= f.text_field :title %>
   </div>
   ```

* f.text\_field
  * Generates input type="text" field
  * Use **:placeholder** hash entry to specify a placeholder (hint) to be displayed inside the field untile the user provideds a value.

  ```
  <div class="field">
    <%= f.label :title, "Heading" %><br>
    <%= f.text_field :title, placeholder: "Have a great title?" %>
  </div>
  ```


* f.text\_area
  * Similiar to **f.text_field**, but for a text area instead of a text field input (default: 40 cols X 20 rows)
  * Can specify a different size (cols X rows) with a **:size** attribute

  ```
  <div class="field">
    <%= f.label :content %><br>
    <%= f.text_area :content, size: "10x3" %>
  </div>
  ```


* Data Helpers

  * f.date\_select
    * Set of select tags (year, month, day) pre-selected for accessing an attribute in the DB. Many formatting options **f.time_select**

  * f.datetime_select

  * distance\_of\_time\_in\_words\_to\_now

  * Many more ...

  * [ActionView::Helpers::DateHelper](http://api.rubyonrails.org/classes/ActionView/Helpers/DateHelper.html



* Other Form Helpers

  Some of these are browser-dependent. Will take advantage of the browsers that are ready for prime time and will still look okay in others.

  * search\_field
  * telephone\_field
  * url\_field
  * email\_field
  * number\_field
  * range\_field


* f.submit

  * Submit button
  * Accepts the name of the **submit button** as its **first argument**
  * If you **don't** provide a name - generates one based on the **model and type of action**, e.g. "Create Post" or "Update Post"
  * [guide](http://guides.rubyonrails.org/form_helpers.html)



#### 2.3.7.2 Layouts

* Layout named **application.html.erb** is **applied by default** as a **shell** for any view template

* Layout that **matches** the name of a controller is **applied** if present (overriding the default layout - application.html.erb)

* You can use **layout** method **inside controller** (outside any action) to **set a layout** for the **entire** controller.

  ```
  layout 'some_layout'
  ```

* You can include a layout for a **specific action** with an **explicit** call to **render** inside the action

  ```
  render layout: 'my_layout'
  ```

 

## 2.4 Security and Nested Resources in Action Pack

### 2.4.1 Github Repository for Module 4

* Each module in the course has a Github repository associated with it. The repository for Module 4 is located [here](https://github.com/jhu-ep-coursera/fullstack-course2-module4-i-reviewed).

* You can find PDFs of the Module 4 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course2-module4-i-reviewed/tree/master/Lectures).

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course2-module4-i-reviewed/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 2.4.2 Nested Resources

#### 2.4.2.1 Nested Resources - Controller

* Create empty notes controller

  ```
  rails g controller notes
  ```


* config/routes.rb

  ```
  Rails.application.routes.draw do
    resources :books do
      resources :notes
    end

    root to: "books#index"
  end
  ```


* table 

| HTTP Method | Named Routes | Parameters | Controller Action | Purpose | 
| --- | --- | --- | --- | --- | 
| GET | book\_notes\_path | Book ID | index | List all | 
| GET | book\_note\_path | Book ID, Note ID | show | Show one | 
| GET | new\_book\_note\_path | Book ID | new | Provide form to input new note | 
| POST | book\_notes\_path | Book ID, Record hash | create | Create new record \(in DB\) | 
| GET | edit\_book\_note\_path | Book ID, Note ID | edit | Provide form to edit record | 
| PUT\/PATCH | book\_note\_path | Book ID, Note ID and Record hash | update | Update record \(in DB\) | 
| DELETE | book\_note\_path | Book ID, Note ID | destroy | Remove record | 


* rake routes 

  ``` 
  $ rake routes 
  ......Prefix     Verb     URI Pattern                                 Controller#Action
  .......notes     GET      /books/:book_id/notes(.:format)             notes#index
  .................POST     /books/:book_id/notes(.:format)             notes#create
  ...new_notes     GET      /books/:book_id/notes/new(.:format)         notes#new
  ..edit_notes     GET      /books/:book_id/notes/:id/edit(.:format)    notes#edit
  .......notes     GET      /books/:book_id/notes/:id(.:format)         notes#show
  .................PATCH    /books/:book_id/notes/:id(.:format)         notes#update
  .................PUT      /books/:book_id/notes/:id(.:format)         notes#update
  .................DELETE   /books/:book_id/notes/:id(.:format)         notes#destroy
  .......books     GET      /books(.:format)                            books#index
  .................POST     /books(.:format)                            books#create
  ...new_books     GET      /books/new(.:format)                        books#new
  ..edit_books     GET      /books/:id/edit(.:format)                   books#edit
  .......books     GET      /books/:id(.:format)                        books#show
  .................PATCH    /books/:id(.:format)                        books#update
  .................PUT      /books/:id(.:format)                        books#update
  .................DELETE   /books/:id(.:format)                        books#destroy
  ........root     GET      / books#index
  ```


* Actions we need for the notes

  * Notes will be shown inline on the **book show page**
  * We don't need all seven actions in the notes controller
  * We just need **create** and **destroy**

  ```
  Rails.application.routes.draw do
    resources :books do
      resources :notes, only: [:create, :destroy]
    end

    root to: "book#index"
  end
  ```

  * You can see the routes update

  ```
  $ rake routes
  ```


* NotesController

  ```
  class NotesController < ApplicationController
    before_action :set_book, only: [:create, :destroy]

    def create
      @note = @book.notes.new(note_params)
      if @note.save
        redirect_to @book, notice: "Note successfully added!"
      else
        redirect_to @book, alert: "Unable to add note!"
      end
    end

    def destroy
      @note = @book.notes.find(params[:id])
      @note.destroy
      redirect_to @book, notice: "note deleted!"
    end

    private
      def set_book
        @book = Book.find(params[:book_id])
      end

      def note_params
        params.require(:note).permit(:title, :note)
      end
  end
  ```


#### 2.4.2.2 Nested Resources - view

* books/show.html.erb - scaffolded

  ```
  <p>
    <strong>Name:</strong>
    <%= @book.name %>
  </p>
  <p>
    <strong>Author:</strong>
    <%= @book.author %>
  </p>

  <%= link_to 'Edit', edit_book_path(@book) %>
  <%= link_to 'Back', book_path %>
  ```

* content_tag helper

  * Nice Rails helper to generate HTML content
  * [content_tag](http://api.rubyonrails.org/classes/ActionView/Helpers/TagHelper.html#method-i-content_tag)
  
  ```
  $ rails c
  >
  > helper.content_tag :p, "hello there"
  => "<p>hello there</p>"
  > helper.content_tag(:div, helper.content_tag(:p, "cool"), class: "world")
  => "<div class=\"world\"><p>cool</p></div>"
  >
  ```


* views/books/show.html.erb

  ```
  <div class="book">
    <%= content_tag :span, "#{@book.name} (#{@book.author})", class: "book-title" %>
    <%= link_to 'Edit', edit_book_path(@book) %>
  </div>
  <%= link_to 'Back', books_path %>
  ```


* Seed some notes - seeds.rb

  ```
  Book.destroy_all
  Book.create! [
    {name: "Eloquent Ruby", authoer: "Russ Olsen"},
    {name: "Beginning Ruby", authoer: "Peter Cooper"}
  ]
  eloquent = Book.find_by name: "Eloquent Ruby"
  eloquent.notes.create! [
    { title: "Wow", note: "Great book to learn Ruby"},
    { title: "funny", note: "Doesn't put you to sleep"}
  ]
  ```


* rake db:seed

  ```
  $ rake db:seed
  ```


* views/notes/\_note.html.erb **partial**

  ```
  <div class="note">
    <div>
      <%= content_tag :span, "#{note.title} (#{time_ago_in_words note.create_at} ago", class: "note-title %>
      <%= link_to "Delete Note", [@book, note], method: :delete %>
    </div>
    <div><%= simple_format note.note %></div>
  ```

  * simple_format will format new lines as <br/>


* views/books/show.html.erb

  ```
  <div class="book">
    <%= content_tag :span, "#{@book.name} (#{@book.author})", class: "book-title" %>
    <%= link_to 'Edit', edit_book_path(@book) %>
  </div>
  <div id="notes">
    <%= render @book.notes %>
  </div>
  <div>
    <%= form_for([@book, @book.notes.new]) do |f| %>
      <div class="field">
        <%= f.lable :title %>
        <%= f.text_field :title %>
      </div>
      <div class="field">
        <%= f.lable :note %>
        <%= f.text_field :note, size: "25x5" %>
      </div>
      <div class="actions">
        <%= f.submit "Add New Note" %>
      </div>
    <% end %>
  </div>
  <%= link_to 'Back', books_path %>
  ```


* application.css

  ```
  .book-title { font: bold 15px arial, sans-serif; }
  .note-title { font: bold 12px arial, sans-serif; }
  .book { padding-bottom: 10px; }
  .note {
    background: lightgray;
    margin: 15px;
    padding: 5px;
    border: 1px solid;
    border-radius: 5px;
    width: 300px;
  }
  # notice  { color: green; }
  #alert   { color: red; }
  .field   { margin: 5px; }
  .actions { margin: 10px 0px }
  ```


### 2.4.3 Authentication

* Authentication

  * To know **who** the user is and if his **credentials** are **valid**


* Authorization

  * Provide **access** only to the books/notes a particular logged-in user is **authorized** to modify/see


* to do

  * Enable (uncomment) **bcrypt-ruby** (Gemfile)
  * Run $bundle (install)
  * restart the rails server
  * add **has_secure_password** to the rescue
  * Make sure **password_digest** is table column
  * Account for **password** (not **password_digest**) inside **strong parameters** list in the controller if you plan to use mass assignment when creating users
  * No need for **password** column in the table (virtual attribute)
 

* reviewer.rb

  ```
  class Reviewer < ActiveRecord::Base
    has_secure_password
    has_many :books
  end
  ```

* schema.rb

  ```
  ActiveRecord::Schema.define(version: yyyymmddxxxxxx) do
    ...
    create_table "reviewers", force: :cascade do |t|
      t.string "name"
      t.string "password_digest"
      t.datetime "created_at", null: false
      t.datetime "updated_at", null: false
    end
    ...
  ```

* Demo
  
  ```
  $ rails c
  >
  > ActiveRecord::Base.logger = nil
  > 
  > Reviewer.column_names
  => ["id", "name", "password_digest", "created_at", "updated_at"]
  >
  > Reviewer.create! name: "Joe", password: "abc123"
  > joe = Reviewer.find_by name: "Joe"
  > joe.authenticate("wrongpassword")
  => false
  > joe.authenticate("abc123")
  => #<Reviewer id: 1, name: "Joe", ... >
  >
  ```

* seeds.rb

  ```
  Reviewer.destroy_all
  Book.destroy_all

  Book.create! [
    {name: "Eloquent Ruby", authoer: "Russ Olsen"},
    {name: "Beginning Ruby", authoer: "Peter Cooper"}
  ]

  eloquent = Book.find_by name: "Eloquent Ruby"
  eloquent.notes.create! [
    { title: "Wow", note: "Great book to learn Ruby"},
    { title: "funny", note: "Doesn't put you to sleep"}
  ]

  reviewers = Reviewer.create! [
    {name: "Joe", authoer: "abc123"},
    {name: "Jin", authoer: "123abc"}
  ]

  Book.all.each do |book|
    book.reviewer = reviewers.sample
    book.save!
  end
  ```


* Check

  ```
  $ rake db:seed
  $ rails c
  > Reviewer.first.books.count
  > Reviewer.last.books.count
  > Reviewer.first.books.pluck :name
  > Reviewer.last.books.pluck :name
  ```



### 2.4.4 HTTP Sessions and Cookies

* HTTP is a stateless protocol

  * Each new request even from the same browser **knows nothing** about the previous request.
  * After a user makes a request, he will be treated as unknown on all the subsequent requests


* Cookies and Sessions to the rescue (keep state)

* [More information](http://guides.rubyonrails.org/security.html#what-are-sessions-questionmark)

* Sessions in Rails

  * Session is created and made available through a **session** hash
  * The server sends the browser a **cookie** with the session information, which the browser **stores** and **sends back** to the server on all subsequent requests (until the session ends)


* Restful Sessions Controller

  * Session can be though of as a resource - let's go ahead and create a RESTful sessions controller

  ```
  $ rails g controller sessions new create destroy -q
  ```

  * routes.rb

  ```
  Rails.application.routes.draw do
    root to: "books#index"

    resources :books do
      resources :notes, only: [:create, :destroy]
    end
    resources :sessions, only: [:new, :create, :destroy]
  end
  ```

  * We can think of **new** action as **login** page and **destroy** action as **logout** page

  * We need **new** (and **create**) actions to create a session and **destroy** action to destroy a session

  * Let's map **login/logout routes** to make this more clear - **routes.rb**

  ```
  Rails.application.routes.draw do
    root to: "books#index"
  
    resources :books do
      resources :notes, only: [:create, :destroy]
    end

    resources :sessions, only: [:new, :create, :destroy]

    get "/login" => "sessions#new", as: "login"
    delete "/logout" => "sessions#destroy", as: "logout"
  end
  ```

    * **as: "login"/"logout"** makes the **_path** and **_url** available for you code. You can use **login_path**/**logout_path** or **login_url**/**logout_url** in your code.

    *  [Custom routes](http://guides.rubyonrails.org/routing.html)


### 2.4.5 Sessions Controller and View

* login page - new.html.erb

  ```
  <h1>Login</h1>
  <%= form_for(:reviewer, url: sessions_path) do |f| %>
    <div class="field"><%= f.flabel :name %><br/> <%= f.text_field :name %></div>
    <p/>
    <div class="field"><%= f.flabel :password %><br/> <%= f.text_field :password %></div>

    <div class="actions"><%= f.submit "Login" %></div>
  <% end %>
  ```

  * form\_for, is using **:reviewer** template, and will sent **post** request to **url: session_path** \(**session** controller's **create** action\)


* sessions\_controller.rb

  ```
  class SessionsController < ApplicationController
    def new
      # Login Page - new.html.erb
    end
    def create
      reviewer = Reviewer.find_by(name: params[:reviewer][:name])
      password = params[:reviewer][:password]

      if reviewer && reviewer.authenticate(password)
        session[:reviewer_id] = reviewer.id
        redirect_to root_path, notice: "Logged in successfully"
      else
        redirect_to login_path, alert: "Invalid username or password"
      end
    end
    def destroy
      reset_session # wipe out session and everything in it
      redirect_to login_path, notice: "You have been logged out"
    end
  end
  ```


* Locking down the application

  * Place **before_action** in the **ApplicationController** (from which all the other controllers **inherit**) that will **make you login** if you are not yet logged in
  * But we cannot block everything. For example, the login page.
  * Place **skip_before_action** to **override** the **before_action** in those special controllers


* application\_controller.rb

  ```
  class ApplicationController < ActionController::Base
    protect_from_forgery with: :exception

    before_action :ensure_login

    protected
      def ensure_login
        redirect_to login_path unless session[:reviewer_id]
      end
  end
  ```


* sessions\_controller.rb

  ```
  class SessionsController < ApplicationController
    skip_before_action :ensure_login, only: [:new, :create]
    def new
      # Login page - new.html.erb
    end
    def create
      ...
    end
    def destroy
      ...
    end
  end
  ```


### 2.4.6 Authorization

* Security Helpers

  * Let's add **logged_in?** and **current_user** helpers to **AppicationController** and make them available as helper methodes to all **controllers** and **views** via **helper_method**.

  * Then, we can add **logic** to **application.html.erb** for logging out and information about the user who is logged in

  ```
  class ApplicationController < ActionController::Base
    protect_from_forgery with: :exception

    before_action :ensure_login
    helper_method :logged_in?, :current_user

    protected
      def ensure_login
        redirect_to login_path unless session[:reviewer_id]
      end
      def logged_in?
        session[:reviewer_id] # nil is false
      end
      def current_user
        @current_user ||=Reviewer.find(session[:reviewer_id])
      end
  end
  ```

  * application.html.erb

  ```
  <!DOCTYPE html>
  <html>
  <head>
  </head>
  <body>

  <% if logged_in? %>
    <div style='float: right;'>
      Logged in as <%= current_user.name %> | 
      <%= link_to "Logout", logout_path, method: :delete %>
    </div>
  <% end %>
  <% flash.each do |key, value| %>
    <p id='<%= key %>'><%= value %></p>
  <% end %>
  <% yield %>
  </body>
  </html>
  ```

* We have **authentication** and we need **authorization**

  * **SOLUTION**: go back to the **BooksController** and **scope things down** based on the **current_user** (instance of **Reviewer**)

* Authorization - index, new, create
  * books\_controller.rb

  ```
  class BooksController < ApplicationController
    before_action :set_book, only: [:show, :edit, :update, :destroy]

    def index
      @books = current_user.books.all
    end
    def new
      @book = current_user.books.new
    end
    def create
      @book = current_user.books.new(book_params)
    end

    private
      def set_book
        @book = current_user.books.find(params[:id])
      end
  end
  ```


### 2.4.7 Pagination

* Shut down the Rails server
* Include **will_paginate** gem
* Run $bundle
* **One** line of code in the **controller**
* **One** line of code in your **view**
* **Restart** your server

* Seed more books

  * seeds.rb

  ```
  Reviewer.destroy_all
  Book.destroy_all

  Book.create! [
    ...
  ]

  100.times { |index| Book.create! name: "Book#{index}", authoer: "Author#{index}" }

  eloquent = Book.find_by name: "Eloquent Ruby"
  eloquent.notes.create! [
    ...
  ]

  reviewers = Reviewer.create! [
    ...
  ]

  Book.all.each do |book|
    book.reviewer = reviewers.sample
    book.save!
  end
  ```

* Clear the cookies in your browser


* books\_controller.rb

  ```
  class BooksController < ApplicationController
    before_action :set_book, only: [:show, :edit, :update, :destroy]

    def index
      @books = current_user.books.paginate(page: params[:page], per_page: 10)
    end
  end
  ```

  * simulate in rails console

  ```
  $ rails c
  >
  > Reviewer.first.books.paginate(page: 3, per_page: 10)
  ```


* books\/index.html.erb

  ```
  <h1>Listing Books</h1>
  <table>
    <thead>
    </thead>
    <tbody>
      <% @books.each do |book| %>
        <tr>
          <td><%= book.name %></td>
          <td><%= book.author %></td>
          <td><%= link_to 'Show', book %></td>
          <td><%= link_to 'Edit', edit_book_path(book) %></td>
          <td><%= link_to 'Destroy', book, method: :delete, data: { confirm: 'Are you sure?' } %></td>
        </tr>
      <% end %>
  </table>
  </p>
  <%= will_paginate @books %>
  <br>
  <%= link_to 'New Book', new_book_path %> 
  ```


### 2.4.8 Deploying to Heroku and Enabling SSL

* Gemfile

  ```
  source 'https://rubygems.org'

  gem 'rails', '4.2.3'
  gem 'sass-rails', '~> 5.0'
  gem 'uglifier', '>= 1.3.0'
  gem 'coffee-rails', '~> 4.1.0'
  gem 'jquery-rails'
  gem 'turbolinks'
  gem 'jbuilder', '~> 2.0'
  gem 'sdoc', '~> 0.4.0', group: :doc

  # Use ActiveModel has_secure_password
  gem 'bcrypt', '~> 3.1.7'

  group :development, :test do
    gem 'byebug'
    gem 'web-console', '~> 2.0'
    gem 'spring'
    gem 'sqlite3'
  end

  group :production do
    gem 'pg'
    gem 'rails_12factor'
  end

  gem 'will_paginate', '~> 3.0.6'
  ```

  * **heroku** use pg DB instead of sqlite


* bundle

  ```
  $ bundle --without production
  ```

  * **--without production** will update the **config** file

  * .bundle\/config

    ```
    BUNDLE_WITHOUT: production
    ```


* push project source code to heroku

  ```
  $ git status
  $
  $ heroku login
  $
  $ heroku create ireview-books
  $ 
  $ git push heroku master
  $
  ```

  * heroku will execute 'bundle install --without development:test


* prepare the DB in heroku

  ```
  $ heroku run rake db:migrate
  $ heroku run rake db:seed
  ```

* enable SSL - https

  * config\/environments\/production.rb

  ```
  config.assets.digest = true
  config.force_ssl = true
  ```

  * each environment has a dedicate config file in **config/environments**


* YOU NEED YOUR OWN **CERITFICATE** to ENABLE SSL for **YOUR OWN DOMAIN**
