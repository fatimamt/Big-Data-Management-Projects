# Mongo DB Cheatsheet
## What is Mongo DB?
"MongoDB is a database management system designed for web applications and internet infrastructure." (MongoDB in Action, 2011).

Open source NoSQL database, which means that catch-all term for databases that generally are not relational and that do not have a query language.

__IMPORTANT__ Mongo DB is document oriented.

## Glosary 
* __Document:__ basic unit of data. Roughly equivalent to a row in a RDBMS.
* __Collection:__ equivalent to a table with a dynamic schema.
* __Databases:__ each of which have its own collections.
* __Cluster:__ 
* __Shell:__ MongoDB comes with an JavaScript shell that allows interaction from the command line.
* MongoDB takes a values as string if "quoted".
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

The general syntaxis is specifying the collection followed by the function/operation to perfom

### > db._name_.insert({"field1":"value1", "field2":"value2", ...})
Inserting a new document to your collection. If the collection does not exist yet, it will be created automatically.As the parameter, give the JSON object you want to insert ([JSON Syntax](https://www.w3schools.com/js/js_json_syntax.asp).

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










