# robomongo

## 1. Script

### 1.1 string field match

```
db.getCollection('spots').find({"root_url" : {$regex : ".*wuxi.*"}}).count()
```

### 1.2 field not empty

```
db.getCollection('spots').find({"spot_star" : {$ne : null}}).count()
```

### 1.3 use variable

```
citynamefilter = ".*shanghai.*";
spotstarfilter = "AAAA.*";
db.getCollection('spots').find({"root_url" : {$regex : citynamefilter}, "spot_star" : {$ne : null}}).count()
db.getCollection('spots').find({"root_url" : {$regex : citynamefilter}, "spot_star" : {$regex : spotstarfilter}}, {"spot_name":1, "spot_star":1, "_id":0}).limit(10)
```
