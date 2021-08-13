# MongoDB 27017

## [Scram Crack](https://github.com/leecybersec/scripting/blob/master/cracking/scram-crack-mongodb.py)

``` bash
$ python3 scram-crack.py 
Tried 1000 passwords
Tried 2000 passwords
Tried 3000 passwords
Tried 4000 passwords
Password found: password123
```

## Connect MongoDB

``` bash
mongo 'mongodb://admin:password123@mongodb0.examples.com'
```

``` bash
mongo --host mongodb0.examples.com --port 28015 -u "alice" -p "password123""
```

## Using MongoDB

Step 1: See all your databases:

``` bash
show dbs
```

Step 2: Select the database

``` bash
use your_database_name
```

Step 3: Show the collections

``` bash
show collections
```

This will list all the collections in your selected database.

Step 4: See all the data

``` bash
db.collection_name.find()
```

``` bash
db.collection_name.find().pretty()
```

## Find and update user

Find `user:1` in collection object

``` bash
db.objects.find({ _key: /^user:1$/ })
```

Update password for `user:1`

``` bash
db.objects.update({ _key: /^user:1$/ }, { $set: { password: "$2y$12$LMqnkbq1FpTnOzAWTgizbugAOpGJaKl0h7PVHvDraW9e0wK2SR7Zu" }})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```