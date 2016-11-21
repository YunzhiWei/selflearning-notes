# Convention

# Plural and singular

* The controllers are named plural and the model is named singular
* Table names in Rails are always named **plural** \(many rows ...\)
* config/initializers/inflections.rb
* In one-to-one association
  * Default name for the foreign key is {master_table_singular}_id, e.g. person_id
* Many to many association needs to create an extra table without a model
  * Plural model names separated by an underscore in **alphabetical** order











