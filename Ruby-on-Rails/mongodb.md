
# System Shell

## Start MongoDB - mongod

```
mongod
```

## Launch MongoDB Shell - mongo

```
mongo
```

## Importing sample data from JSON file

```
C:\> mongoimport --db test --collection zips --drop --file zips.json
```

# Mongo Shell

## Switch to test Database

```
> use test
```

## find command

```
> db.zips.findOne()
```

## Create Collection

  * Fixed-size

  ```
  db.createCollection("log", { capped : true, size : 5242880, max : 5000 } )
  ```

# IRB Shell

## Using gem in IRB

```
> require 'mongo'
```

## Set IRB log output level

```
> Mongo::Logger.logger.level = ::Logger::INFO
```

## Connect to Mongo DB

```
> db = Mongo::Client.new('mongodb://localhost:27017')
> db = db.use('test')
```

## Use system command in IRB shell

```
> system('cls')
```

## Basic MongoDB command in IRB

```
> db = db.use('test')
> db.database.name
> db.database.collection_names
> db[:zips].find.first
```

### Insert/Create

* insert_one

```
db[:zips].insert_one(:_id=>"100", :city=>"city01", :loc=>[-74.05, 37.56], :pop=>4678, :state=>"MD")
```

* insert_many

```
db[:zips].insert_many([
    {:_id=>"200", :city=>"city02", :loc=>[-74.05, 37.56], :pop=>2000, :state=>"CA")},  
    {:_id=>"300", :city=>"city03", :loc=>[-74.05, 37.56], :pop=>3000, :state=>"CA")},  
  ])
```

* find/count

```
db[:zips].find(:city=>"city01").count
```


# Rails console

```
> mongo_client=Mongoid::Clients.default
> mongo_client.database.name
> collection=mongo_client[:zips]
> collection.count
```


# Mongo Field Type

  - String
  - Integer
  - BigDecimal
  - Float
  - Boolean
  - Time
  - TimeWithZone
  - DateTime
  - Date
  - Hash
  - Array
  - Symbol
  - BSON
  - Range
  - Regexp
