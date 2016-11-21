# ORM

# 8. Timestamps

## How to include
```
      class Race 
        include Mongoid::Document
        include Mongoid::Timestamps
```

## What we have after include it
* created_at
* updated_at

## Exception when no 'Timestamp' included
* You always need to have time stamp to access a specific resource.
* Else, error will happen


