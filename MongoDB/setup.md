To install mongodb in mac (using brew):

> `brew tap mongodb/brew`

> `brew install mongodb-community`


To start or stop the server:
> `brew services start mongodb-community`

> `brew services stop mongodb-community`

Connect using Mongoshell: 

> `mongosh`  
(by default connects to mongo server running in localhost at port 27017)

> `mongoimport -d db_name -c coll_name --file <file_name>.json --jsonArray`  
(it appends data to pre-existing collection if any, '--drop' flag can be used to overwrite pre-existing collection)

Basic Mongosh commands:
> `show dbs`  
(list all databases with non 0 size, i.e., if you create use a database that doesn't have a collection then it won't show in this command output)

> `use db_name`  
(connects to db_name)

> `db`  
(shows current connected database)

> `show collections`  
(shows all connections in current db being used)

> `db.coll_name.find()`   
(returns all collections in the collection coll_name)

> `db.coll_name.insertOne(<document>)`    
(insert document in collection)

> `db.coll_name.createIndex(<index_document>)`  
(creates index)

> `db.coll_name.getIndexes()`  
(returns all indexes)

> `db.coll_name.dropIndex(<index_document/name>)`  
(drops given index)

> `db.createCollection("coll_name")`  
(creates collection with given name inside current  connected db)

