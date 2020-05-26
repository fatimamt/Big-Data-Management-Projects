# Mongo DB Cheatsheet
## What is Mongo DB?
"MongoDB is a database management system designed for web applications and internet infrastructure." (MongoDB in Action, 2011).

Open source NoSQL database, which means that catch-all term for databases that generally are not relational and that do not have a query language.

__IMPORTANT__ Mongo DB is document oriented.

## Glosary and important points
* __Document:__ basic unit of data. Roughly equivalent to a row in a RDBMS.
* __Collection:__ equivalent to a table with a dynamic schema.
* __Databases:__ each of which have its own collections.
* __Cluster:__ 
* __Shell:__ MongoDB comes with an JavaScript shell that allows interaction from the command line.
* __Method:__ 
* __Operator:__ Always starts with a $.
* __nRemoved:__ Number of documents deleted.
* __nMatched:__ Number of documents matched.
* __nUpserted:__ Number of documents that were created.
* __nModified:__ Number of documents modified.
* __log:__
* MongoDB takes a values as string if "quoted".
* You can add a date type for a value typing _new Date(year, month, day)_.
* Furthermore, you can store any data type within an array.
* Documents can be embedden within another by adding the document as a value for a given field.
* 

## Install
To install MongoDB to work from the shell, clic the [link](https://www.mongodb.com/download-center/community) to download it and in the [guide](https://docs.mongodb.com/guides/server/install/) to install it. If you want to use MongoDB online, you can use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

## 1. Get Started

__Access the MongoDB database using shell__
When initialazing in MongoDB, the sorce gives the options to work from the shell, locally, or online in [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

Once the cluster where you will work in is created, connect locally in the shell writing ___mongo --___ followed by the access to the database. For this document, I will be using the provided by my professor.

![Initialize](Cheatsheet/Init.png)

If needed, enter the password.
### > show dbs
To show all the databases. This list shows the name and size of the databases

![showdbs](Cheatsheet/showdbs.png)

### > use _dbname_
To switch to an specific database.

![use](Cheatsheet/usetest.png)

### > db
To see the database is currently assigned.

![db](Cheatsheet/db.png)

### > db.createCollection("_name_")
Create a new collection in the database.

![createCollection](Cheatsheet/createCollection.png)

### > show collections
To show all the collections in the database. You can use _show tables_ instead and the output is the same.

![show collections](Cheatsheet/collections.png)

### > help
To show a menu with more commands you may need and would like to give it a check.

![help](Cheatsheet/help.png)

## 2. Insert Documents
An unique _ _id_ field is given when a document is inserted using the ObjectId data Type.

The general syntaxis is specifying the collection followed by the method to perfom

### > db._name_.insert({"field1":"value1", "field2":"value2", ...})
Inserting a new document to your collection. If the collection does not exist yet, it will be created automatically.As the parameter, give the JSON object you want to insert ([JSON Syntax](https://www.w3schools.com/js/js_json_syntax.asp)).

![insert](Cheatsheet/insert.png)

If the message _WriteResult({ "nInserted": 1 })_ appears, the documment was successfully inserted.

You can also use

\> db._name_.insertOne({"field1":"value1", "field2":"value2", ...})

or

\> db._name_.insertMany(\[{"field1":"value1",...},{"field2":"value2",...},...\])

to insert more than one document at the same time.

## 3. Find Documents

### > db._name_.find()
To see which documents the collection contains.

![find](Cheatsheet/find.png)

### > db._name_.find().pretty()
To format the results of the collection.

![pretty](Cheatsheet/pretty.png)

### > db._name_.find({"field":"value"}).pretty()
If you look for an specific field in your documents, express the values inside the operation writing the field and value.

![find()](Cheatsheet/find().png)

### > db._name_.find({"field.fieldembedded":"value"}).pretty()
To search for a field embedded into anothe document, you can use dot dotation to specify the embedded field you would like to search. The number of dots depends on the number of "levels" you have to pass through to get the desired field.

![dotnotation](Cheatsheet/dotnotation.png)

## 4. Delete

### > db._name_.remove({"field":"value"})
This method will delete documentch that match with the query.

![remove](Cheatsheet/remove.png)

If the message _WriteResult({ "nRemoved": 1 })_ appears, the document(s) was/were successfully deleted.

## Update data

### > db._name_.update({"field1":"value1"}, {"$set":{"field2":"newvalue"}})
If you want to update some values in ypur collection, you use the update method which envolves a pair of brackets, that states the query parameter, a second pair of brackets which contains the update parameter with the "$set" operator to update all the matching documents.

If the message _WriteResult({ "nMatched": 1, "nUpserted": 0, "nModified": 1  })_ appears, the document(s) was/were successfully updated.

![set](Cheatsheet/set.png)

When the "$set" operator is not stated and the content inside the parenthesis goes of the kind of _{"field1":"value"},{"field2:"newvalue"}_ the data will be imported to the document.

### > db._name_.update({"field1":"value1"}, {"$set":{"field2":"newvalue"}}, {"multi":true})
To update multiple documents, the third parameter "multi" must be of the kind _true_ to modified all matching documents.

![multi](Cheatsheet/multi.png)

### > db._name_.update({"field1":"value1"}, {"$inc":{"field2":_number_}})
To increment a field by a specific value, you must use the "$inc" operator. The number will be the times the field is incremented (or decremented if using negative numbers) to.

![inc](Cheatsheet/inc.png)

If the field does not exists, it gets created with the value.

### > db._name_.update({"field1":"value1"}, {"$inc":{"field2":_number_}}, {"upsert":true})
When the "upsert" option is equal to _true_, the document either is updated or created if the field does not exist. This option creates a document using the values from the query and update parameter.

![upsert](Cheatsheet/upsert.png)

"nUpserted" field of the WriteResult message must increment to know that the document(s) was/were successfully created. Otherwise, if that field is equal to 0 but both "nMatched" and "nModified" are different of zero, then the document(s) was/were successfully updated.

### > db._name_.update({}, {"$unset":{"field1":""}}, {"multi":true})
__Note__ If the query parameter (first pair of brackets) is empty, that means that all the documents of the collection will be taken. Similarly, if the value of the field to update is not stated, it takes all the values of that field.

This command is to remove specified fields from all documents the query match (thanks to the "multi"":true option) due to the "$unset" operator.

![unset](Cheatsheet/unset.png)

### > db._name_.update({}, {"$rename":{"field":"newfield"}}, {"multi":true})
If what you want is to change field names, you can use the "$rename" operator. Inside its brackets, for the value you have to open a new pair of brackets to specified the field you want to rename, followed by : and the new field name.

![rename](Cheatsheet/rename.png)














