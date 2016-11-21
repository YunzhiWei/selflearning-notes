# Console Command

# 1. Rails Command

## 1.1 New application

* Command:
```
$ rails new [*application name*]
```

* \[application name\] is start in lower case, plural
* Often stuck in the step of 'bundle install', because 'bundle install' will go to 'rubygems.org' to check update
* Can be solved by the following commands
```
$ rails new my_app --skip-bundle
$ cd my_app
$ bundle install --local
```


## 1.2 Generate a mongoid.yml configuration file

* Command:
```
$ rails g mongoid:config
```

* 'mongoid.yml' is in config folder


## 1.3 Generate new model & migration

* Command:
```
$ rails g scaffold [module/table name] [column name]:[datatype]
```


## 1.4 Generate new Mongoid model

* Command:
```
$ rails g model [model name] [column name]:[datatype]
```


## 1.5 Start rails console

* Command:
```
$ rails c
```
_Or_
```
$ irb
```


## 1.6 start rails server

* Command
```
$ rails s
```


----


# 2 Rake command

## 2.1 database migration/rollback

* Command
```
$ rake db:migrate
$ rake db:rollback
```

## 2.2 database initial

* Command
```
$ rake db:seed
```


## 2.3 db/schema.rb

* the snapshot of your latest database

* command to apply the schema to a new environment

```
$ rake db:schema:load
```




## 2.4 database initial by tasks

* Command
```
$ rake [rake file name in lib/tasks folder]:[task name in rake file]
```


## 2.5 check routes

* Command
```
$ rake routes
```
_or_
```
$ rake routes | grep [string pattern]
```

### 2.6 Execute tasks

* Command:
```
$ rake assignment:setup_data
```

* There is one 'assignment.rake' file in 'lib\/tasks' folder

* There is one task named 'setup\_data' in 'assignment.rake'


----


# 3. db console command

## 3.1 start db console

* Command
```
$ rails db
```

## 3.2 DB Console command

* help
```
sqlite> .help
```


* table
```
sqlite> .tables
```


* table schema
```
sqlite> .schema cars
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



* table columns

> If you are comfortable with SQL commands, you can enter your app's folder and run rails db, which is a brief form of rails dbconsole. It will enter the shell of your database, whether it is sqlite or mysql.
> 
> Then, you can query the table columns using sql command like:

```
sqlite> pragma table_info(your_table);
```


---


# 4. Rails Console

## 4.1 start Rails console

* Command
```
$ rails c
```

## 4.2 Reload

* Command
```
> reload!
```


## 4.3 System command

* Command
```
> system('{system console command}')
```
* {System console command}, for example, 'clear'


## 4.4 Disable logger

* Command
```
> ActiveRecord::Base.logger = nil
```


----


# 5. MongoDB Console

## 5.1 MongoDB Install

Visit [Mongo Web Site](https://www.mongodb.org/)

1. Follow the instruction 'Instructions for installing with Homebrew' from [here](https://www.mongodb.com/download-center#community)
```
$ brew update
$ brew install mongodb
$ sudo mkdir -p /data/db
$ cd /data
$ sudo chmod -R 777 db
```

2. Start MongoDB server
```
mongod
```


## 5.2 Import Example Data

1. Download the [zips.json](http://media.mongodb.org/zips.json)

2. Import data by the following command
```
$ mongoimport --db test --collection zips --drop --file zips.json
```


## 5.3 Simple Operation

* Start Mongo Shell
```
$ mongo
```

* Switch Database
```
> use test
```

* Basic Command

  * findOne
  ```
  db.zips.findOne()
  ```


## 5.4 MongoDB Ruby Driver Setup

### 5.4.1 mongo-ruby driver
```
gem update --system
gem install mongo
gem install bson_ext
```

### 5.4.2 Using gem in irb shell

* Start irb shell
```
$ irb
```

* Basic commands
```
> require 'mongo'
> Mongo::Logger.logger.level = ::Logger::INFO
> db = Mongo::Client.new('mongodb://localhost:27017')
> db=db.use('test')
> db.database.name
> db.database.collection_names
> db[:zips].find.first
>
```

