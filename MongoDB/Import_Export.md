# MongoDB Import and Export

Copy from [here](https://www.mkyong.com/mongodb/mongodb-import-and-export-example/)

In this tutorial, we show you how to backup and restore MongoDB with the commands : mongoexport and mongoimport.

## 1. Backup database with mongoexport
Few examples to show you how to use the mongoexport to back up the database.

Review some of the common use options.

```
$ mongoexport
Export MongoDB data to CSV, TSV or JSON files.

options:
  -h [ --host ] arg         mongo host to connect to ( <set name>/s1,s2 for
  -u [ --username ] arg     username
  -p [ --password ] arg     password
  -d [ --db ] arg           database to use
  -c [ --collection ] arg   collection to use (some commands)
  -q [ --query ] arg        query filter, as a JSON string
  -o [ --out ] arg          output file; if not specified, stdout is used
```

### 1.1 Export all documents (all fields) into the file `domain-bk.json`.

```
$ mongoexport -d webmitta -c domain -o domain-bk.json
connected to: 127.0.0.1
exported 10951 records
```

### 1.2 Export all documents with fields `domain` and `worth` only.

```
$ mongoexport -d webmitta -c domain -f "domain,worth" -o domain-bk.json
connected to: 127.0.0.1
exported 10951 records
```

### 1.3 Export all documents with a search query, in this case, only document with `worth > 100000` will be exported.

```
$mongoexport -d webmitta -c domain -f "domain,worth" -q '{worth:{$gt:100000}}' -o domain-bk.json
connected to: 127.0.0.1
exported 10903 records
```

### 1.4 Connect to remote server like `mongolab.com`, using `username` and `password`.

```
$ mongoexport -h id.mongolab.com:47307 -d heroku_app -c domain -u username123 -p password123 -o domain-bk.json
connected to: id.mongolab.com:47307
exported 10951 records
```

Review the exported file.

```
$ ls -lsa
total 2144
   0 drwxr-xr-x   5 mkyong  staff      170 Apr 10 12:00 .
   0 drwxr-xr-x+ 50 mkyong  staff     1700 Apr  5 10:55 ..
2128 -rw-r--r--   1 mkyong  staff  1089198 Apr 10 12:15 domain-bk.json
```

> **Note**

> With mongoexport, all exported documents will be in json format.


## 2. Restore database with mongoimport

Few examples to show you how to use the mongoimport to restore the database.

Review some of the common use options.

```
$ mongoimport
connected to: 127.0.0.1
no collection specified!
Import CSV, TSV or JSON data into MongoDB.

options:
  -h [ --host ] arg       mongo host to connect to ( <set name>/s1,s2 for sets)
  -u [ --username ] arg   username
  -p [ --password ] arg   password
  -d [ --db ] arg         database to use
  -c [ --collection ] arg collection to use (some commands)
  -f [ --fields ] arg     comma separated list of field names e.g. -f name,age
  --file arg              file to import from; if not specified stdin is used
  --drop                  drop collection first
  --upsert                insert or update objects that already exist
```

### 2.1 Imports all documents from file `domain-bk.json` into `database.collection` named `webmitta2.domain2`. All non-exists databases or collections will be created automatically.

```
$ mongoimport -d webmitta2 -c domain2 --file domain-bk.json
connected to: 127.0.0.1
Wed Apr 10 13:26:12 imported 10903 objects
```

### 2.2 Imports all documents, insert or update objects that already exist (based on the `_id`).

```
$ mongoimport -d webmitta2 -c domain2 --file domain-bk.json --upsert
connected to: 127.0.0.1
Wed Apr 10 13:26:12 imported 10903 objects
```

### 2.3 Connect to remote server – `mongolab.com`, using `username` and `password`, and import the documents from the local file `domain-bk.json` into remote MongoDB server.

```
$ mongoimport -h id.mongolab.com:47307 -d heroku_app -c domain -u username123 -p password123 --file domain-bk.json
connected to: id.mongolab.com:47307
Wed Apr 10 13:26:12 imported 10903 objects
```

## 3 Real Case

```
mongoexport -h ds133418.mlab.com:33418 -d resortplace -c spots -u resortplace -p cncn -o wuxi.json -f "spot_name,spot_star,spot_addr" -q "{root_url: {$regex: '.*wuxi.*'}}"
```

## References

[MongoDB Official Doc – Importing and Exporting MongoDB Data](http://docs.mongodb.org/manual/core/import-export/)
