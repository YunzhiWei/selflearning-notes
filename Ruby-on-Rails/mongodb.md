
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
