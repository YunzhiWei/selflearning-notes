# 3. Ruby on Rails Web Services and Integration with MongoDB



## 3.1 Introduction to MongoDB, MongoDB-Ruby API, and CRUD



### 3.1.1 Github Repository for Module 1



* Please click the link below to access the Github repository for Module 1.

> https://github.com/jhu-ep-coursera/fullstack-course3-module1-zips



* Please click the link below to access PDF versions of all lecture slides in Module 1.

> https://github.com/jhu-ep-coursera/fullstack-course3-module1



### 3.1.2 Introduction to NoSQL

### 3.1.3 Categories of NoSQL

### 3.1.4 Introduction to MongoDB

### 3.1.5 Mongo Installation

#### 3.1.5.1 Install MongoDB

* Download MongoDB (msi) from [here](https://www.mongodb.com/download-center)
* Prepare for the DB folder (the default folder is C:\data\db)

#### 3.1.5.2 Configure MongoDB

#### 3.1.5.3 Start MongoDB - mongod

**Please run this command in C:\data\db folder**

```
mongod
```

#### 3.1.5.4 Launch MongoDB Shell - mongo

```
mongo
```

### 3.1.6 MongoDB Basics

#### 3.1.6.1 Importing sample data

* download [zips.json](http://media.mongodb.org/zips.json?_ga=1.42259692.837974793.1480646114) file from MongoDB
* import data with the following command in **windows command shell**

```
C:\> mongoimport --db test --collection zips --drop --file zips.json
```

#### 3.1.6.2 Basics of MongoDB shell

* Start mongo shell

```
C:\> mongo
```

* Switch to test Database

```
> use test
```

* find command

```
> db.zips.findOne()
```

#### 3.1.6.3 MongoDB collections

* Collection Types
  * Fixed-size

  ```
  db.createCollection("log", { capped : true, size : 5242880, max : 5000 } )
  ```

#### 3.1.6.4 IRB shell and MongoDB

* mongo-ruby dirver

```
gem update -system
gem install mongo
gem install bson_ext
```

* Start IRB shell

```
> IRB
```

* Using gem in IRB

```
> require 'mongo'
```

* Set IRB log output level with the following command to get rid of debugging information

```
> Mongo::Logger.logger.level = ::Logger::INFO
```

* Connect to Mongo DB

```
> db = Mongo::Client.new('mongodb://localhost:27017')
> db = db.use('test')
```

* Use system command in IRB shell

```
> system('cls')
```

#### 3.1.6.5 Basic MongoDB command in IRB

```
> db = db.use('test')
> db.database.name
> db.database.collection_names
> db[:zips].find.first
```

### 3.1.7 Inserting Documents


#### 3.1.7.1 insert_one

```
db[:zips].insert_one(:_id=>"100", :city=>"city01", :loc=>[-74.05, 37.56], :pop=>4678, :state=>"MD")
```

#### 3.1.7.2 insert_many

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

#### "\_id" field

* primary key for every Document
* default field for the BSON object and is indexed automatically
* You can add a custom "id" filed if you like (but different from the default \_id)


### 3.1.8 Find

### 3.1.9 Paging

### 3.1.10 Advanced Find

### 3.1.11 Replace, Update, and Delete

### 3.1.12 Introduction: Integrating MongoDB with Ruby Driver

### 3.1.13 Rails Setup

#### 3.1.13.1 Rails Setup

* Create new Application

```
rails new zips
```

* Add mongoid gem to Gemfile

```
gem 'mongoid', '~> 5.0.0'
gem 'will_paginate', '~> 3.0.7'
# add this extra Gemfile to add will_paginate support for mongoid
gem 'will_paginate_mongoid', '~> 2.0.1'
```

* Run 'bundle' to install gem in the current project

```
bundle
```

* Mongo database configuration

```
rails g mongoid:config
```

**config/mongoid.yml** will be created by the above command.

* Check mongoid.yml file about the database connection information

* Check **config/application.rb** file (this is the bootstraps mongoid within application -- like rails console)

```
#bootstraps mongoid within applications -- like rails console
Mongoid.load!('./config/mongoid.yml')

#which default ORM are we using with scaffold
#add  --orm none, mongoid, or active_record
#    to rails generate cmd line to be specific
# config.generators {|g| g.orm :active_record}
# config.generators {|g| g.orm :mongoid}
```

#### 3.1.13.2 Test mongoid in rails console

* In system shell, type the following command

```
rails c
```

* In rails console, type the following commands

```
> mongo_client=Mongoid::Clients.default
> mongo_client.database.name
> collection=mongo_client[:zips]
> collection.count
```

### 3.1.14 DAO Class Infrastructure

### 3.1.15 CRUD

### 3.1.16 Scaffolding

#### 3.1.16.1 Model mixin

```
class Zip
  include ActiveModel::Model
  ... ...
  def persisted?
    !@id.nil?
  end
  def created_at
    nil
  end
  def updated_at
    nil
  end
```

#### 3.1.16.2 Scaffold command

```
rails g Scaffold_controller Zip id city state population:integer
```

#### 3.1.16.3 Helpers

```
module ZipHelper
  def toZip(value)
    return value.is_a?(Zip) ? value : Zip.new(value)
  end
end
```

### 3.1.17 MVC Application

### 3.1.18 MongoLab Setup

### 3.1.19 Heroku Setup

* mongoid.yml (to use Environment Variable)

```
uri: <%= ENV['MONGOLAB_URI'] %>
```

* set Environment Variable in Heroku

```
> heroku config:add MONGOLAB_URI=mongodb://<dbuser>:<dbpassword>@ds017205.mlab.com:17205/universal
```

## 3.2 Aggregation Framework, Performance, and Advanced MongoDB



### 3.2.1 Github Repository for Module 2



* Github repository for Module 2 -

> https://github.com/jhu-ep-coursera/fullstack-course3-module2



* Github repository for Module 2: GridFS Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module2-gridfs



* Github repository for Module 2: GridFS Web Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module2-gridfsfiles



* Github repository for Module 2: GeoZips Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module2-geozips



### 3.2.2 $project

### 3.2.3 $group

### 3.2.4 $match

### 3.2.5 $unwind

### 3.2.6 Schema Design

### 3.2.7 Normalization

### 3.2.8 Relationships

### 3.2.9 GridFS

### 3.2.10 GridFS Demo 1

### 3.2.11 GridFS Demo 2

### 3.2.12 GridFS Demo 3

### 3.2.13 Geospatial

### 3.2.14 Geospatial Demo

### 3.2.15 Introduction to Indexes

### 3.2.16 Creating Indexes

### 3.2.17 Listing & Deleting Indexes

### 3.2.18 Unique, Sparse & TTL Indexes



## 3.3 Mongoid



### 3.3.1 Github Repository for Module 3



* Github repository for Module 3 -

> https://github.com/jhu-ep-coursera/fullstack-course3-module3



* Github repository for Module 3: Movies Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module3-movies







### 3.3.2 Introduction to Mongoid

### 3.3.3 Document Class

#### 3.3.3.1 Documents

* Documents are the **core** object in Mongoid

```
Mongid::Document
```

* Documents can be stored in a collection or embedded in other Documents

```
class Movie
  include Mongoid::Documents
end
```

#### 3.3.3.2 Fields

* Fields are **attributes**, default type is Strings

```
class Movie
  include Mongoid::Documents
  field :title, type: String
  field :type, type: String
  field :rated, type: String
  field :year, type: Integer
end
```

* OS shell command to generate a model

```
rails g model
```

Example

```
rails g model Movie title type rated year:Integer rlease_date:date \
                    runtime:Measurement votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```

```
rails g model Actor name birth_name date_of_birth:Date height:Measurement bio:text
```

#### 3.3.3.3 Timestamps

* Include timestamp

  ```
class Movie
  include Mongoid::Documents
  include Mongoid::Timestamps
end
  ```

  - created_at and updated_at fields will be added
  - **touch** method will update the document's updated_at field

#### 3.3.3.4 Mongo Field Type

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

#### 3.3.3.5 Field Aliases

  ```
class Movie
  include Mongoid::Documents
  ... ...
  field :birthName, as: :birth_name, type: String
  ... ...
end
  ```

* birthName (camel case) in document -> mapped to birth_name (rails uses snake case) in model
* Comply with rails naming convertion
* Helps during compression

#### 3.3.3.6 Customer Fields (Very Important) (to do more learning later)

#### 3.3.3.7 store_in

```
class Location
  include Mongoid::Documents
  ... ...
  store_in collection: "places"
  ... ...
end
```

* Application type to Document type mapping
* Location gets stored in to "places" collection


### 3.3.4 Mongoid CRUD

### 3.3.5 Movie Application Setup

#### 3.3.5.1 Initialization

* Import data

```
rake db:seed
```

json files in the 'db' folder

* Setup index

```
rake db:mongoid:create_indexes
```

index information is stored in the model class

```
class Location
  include Mongoid::Documents
  ... ...
  index ({ :"place_of_birth.geolocation" => Mongo::Index::GEO2DSPHERE})
  ... ...
end
```

#### 3.3.5.2 Customer Types (Import) (to do more learning)

#### 3.3.5.3 Model Types and Document Representations

* Place
* Actor
* Writer
* Director
* Movie

#### 3.3.5.4 Document Model Class

* DirectorRef - is an **annotated** reference to a Director
* MovieRole - is a charactor in a **Movie** played by an **Actor**

### 3.3.6 1:1 Embedded Relationship

### 3.3.7 M:1 Linked Relationship

### 3.3.8 1:M Embedded Relationship

### 3.3.9 M:1 Embedded Relationship

### 3.3.10 1:1 Linked Relationship

### 3.3.11 M:M Linked Relationship

### 3.3.12 Constraints and Validation

### 3.3.13 Constraints and Validation: Demo

### 3.3.14 Queries (Find)

### 3.3.15 Queries (Where)

### 3.3.16 Pluck and Scope

### 3.3.17 Scaffolding

#### 3.3.17.1 Basic Steps

* OS command shell

```
> rails new Movies
> cd movies
```

* Update Gemfile

```
gem 'mongoid', '~> 5.0.0'
```

* bundle

```
> bundle
```

* Generate mongoid.yml

```
> rails g mongoid:config config/mongoid.yml
```

* Start the Server

```
> rails s
```

#### 3.3.17.2 Custom Class and Methods

* Measurement
* Point
* initialize - normalized form -- independent of source formats
* to_s - useful in producing formatted output
* mongoize - creates a DB form of the instance
* self.demongoize(object) - creates an instance of the class from the DB-form of the data
* self.mongoize(object) - takes in all forms of the object and produces a DB-friendly form
* self.evolve(object) - used by criteria to convert object to DB-friendly form

#### 3.3.17.3 Scaffolding (Important) (to do more learning)

* Note: mongoid is the default model generator.
  - To be explicit at command time, add the **--orm mongoid** option to the command line.

##### model

* Place

Place models a point and its descriptive address information

```
rails g model Place formatted_address geolocation:Point street_number street_name city postal_code county state country
```

* Director

Director models the detailed information of a movie director

```
rails g model Director name
```

* DirectorRef

DirectorRef is an annotated reference to a director taht gets embedded into the Movie

```
rails g model DirectorRef name
```


* Writer

Writer holds the detailed information about the writer of a Movie
This class is directly associated with the movie without an annotated link

```
rails g model Writer name
```

* Actor

Actor contains the information details of and actor in a Movie

```
rails g model Actor name birth_name date_of_birth:Date height:Measurement bio:text
```


* MovieRole

MovieRole holds the role-specific information and relation between the Movie and Actor

```
rails g model MovieRole character actor_name main:boolean url_character url_photo url_profile
```


* Movie

Movie holds the role information about Movie, its properties, and supporting members

```
rails g model Movie title type rated year:Integer rlease_date:date \
                    runtime:Measurement votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```


##### Controller and View - Assembly

```
rails g Scaffold_controller Movie title type rated year:Integer rlease_date:date \
                    runtime:integer votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```


```
rails g Scaffold_controller Movie title type rated year:Integer rlease_date:date \
                    runtime:integer votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```


```
rails g Scaffold_controller Movie title type rated year:Integer rlease_date:date \
                    runtime:integer votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```


```
rails g Scaffold_controller Movie title type rated year:Integer rlease_date:date \
                    runtime:integer votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```


```
rails g Scaffold_controller Movie title type rated year:Integer rlease_date:date \
                    runtime:integer votes:integer countries:array languages:array \
                    genres:array filming_locations:array metascore simple_plot:text \
                    plot:text url_imdb url_poster directors:array actors:array
```

#### 3.3.17.4 Routes

* routes.rb

```
resources :movies
```

## 3.4 Web Services



### 3.4.1 Github Repository for Module 4



* Github repository for Module 4 -

> https://github.com/jhu-ep-coursera/fullstack-course3-module4



* Github repository for Module 4, Lesson 2 -

> https://github.com/jhu-ep-coursera/fullstack-course3-module4-wsmovies



* Github repository for Module 4: Caching Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module4-caching_movies



* Github repository for Module 4: OAuth 2 Demo -

> https://github.com/jhu-ep-coursera/fullstack-course3-module4-oauth_movies



### 3.4.2 Introduction to Web Services

### 3.4.3 REST and RMM

### 3.4.4 Resources

### 3.4.5 URIs

### 3.4.6 Nested URIs

### 3.4.7 Query Parameters

### 3.4.8 Methods

### 3.4.9 Idempotence

### 3.4.10 Representations

### 3.4.11 Versioning

### 3.4.12 Content Negotiations

### 3.4.13 Headers and Status

### 3.4.14 Client Caching

### 3.4.15 Cache Revalidation Headers

### 3.4.16 Cache Controls

### 3.4.17 Server Caching

### 3.4.18 OAuth2

### 3.4.19 Assembly

### 3.4.20 Devise

### 3.4.21 Integrated Authentication

### 3.4.22 OAuth Integration
