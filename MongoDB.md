---
title: MongoDB
description: 
published: true
date: 2021-05-13T17:33:07.176Z
tags: mongodb, database, nosql, mongoose
editor: markdown
dateCreated: 2020-06-04T20:56:01.677Z
---

![MongoDB](https://digitizor.com/wp-content/uploads/2012/02/mongo-db-huge-logo-1024x341.png =300x100){.align-left}is a **NoSQL** database.
It has a '*Database*' with '*Collections*' which has each '*Documents*'.
A document is in JSON format, with an unique ID (***ObjectId***).

---

# Command-Liners

## Databases:

```js
// show all databases: 
show databases;
```
```js
// 'connects' to a database:
use Database_name;
```
---
## Collections:
every databases has one ore more collections:

```js
// shows all collections within a database (first use the use Database_name command)
show collections;
```
---
## Searching:
You can search(find) in exact key value pair.
> **If you want to search all values on your input, you have to create an Index, see below for an example**
{.is-success}
### Create an Index
```js
// connect to a Database
use database_name;
// this will index all values within a collection
db.collection_name.createIndex( { "$**" : "text" } );
```

### Show all indexes of a collection:

```js
db.collection.getIndexes()
``` 


### Drop all indexes of a collection:

```js
db.collection.dropIndexes()
``` 
---
## Find
```js
// shows all documents inside the collection
db.collection_name.find();
// pretties the output:
db.collection_name.find().pretty();
```
```js
// Search on exact key and value pair:
db.collection_name.find({"Key": "Value"})
```
```js
// Nested search with "dot notation"
db.collection_name.find({"Key.nestedKey": "Value"})
```
---

## (Advanced) Query
Assuming you already created an text index in your collection.
With the following command you can query your collection.
The quotes are intented, with this format it will query:

**Microsoft .NET Framework** `AND` **4.6.2**
if you leave the quotes away every word will be queried with `OR`

```bash
db.CVE.find({$text: {$search: "\"Microsoft .NET Framework\" \"4.6.2\""}}).pretty()
```

---

> After some researching about speeding up my queries i found out the `AND` operator,which gives the best results is also the slowest form of searching/quering.
{.is-warning}

I found out it will query all the documents to match the criteria, you need to flip it around, **filter** your search each step with a álà playbook style, see below for an example, you can regex what you want and build more `AND` steps along the way.




```bash
db.Collection.find({
	$and: [{
  	$text: {
    	$search: "your search query"
		}
	},
	{
		"text.path.to.search": {
			$regex: /your search query/i
		}
	}]
})
```

> The regex: `/your search query/i` , will an exact search over the first `$text` search
{.is-success}


----

## Manipulate data within the shell
Use `patch` to change a single field without touching the other (possible) nested key - value pairs.

```bash
Example
```

with `update` you won't only change the field but complete replacement

```bash
Example
```

The following commands deletes document(s) out of your collection:
```bash
# Delete one document:
db.collectio_Name.delete
```
``` bash
# 'deleteMany' to delete multi documents at once
db.collection_Name.deleteMany
```


---
## Rename Collection

db.collection_name.renameCollection("New_Collection_Name")

---
## Drop Collection or Database
> WARNING: THIS CANNNOT BE UNDONE
{.is-danger}

Dropping collection:
```bash
db.collection_name.drop()

```

Dropping databse:
```bash
use database_name
db.dropDatabase()
```


# Mongoose

is the DB connector for nodejs, it let use predefined structures with conditions (aka schemas).
This examples if from [Feathers](/Feathers):
```js
module.exports = function (app) {
  const modelName = 'questions';
  const mongooseClient = app.get('mongooseClient');
  const { Schema } = mongooseClient;
  const schema = new Schema({
    questionNumber: {type: Number},
    category: {type: String},
    //Explained below
    user_id: { type: Schema.Types.ObjectId, ref: 'users' },
    question: { type: String, required: true },
    right_answer: { type: Number, required: true },
    answers: [String],
    startTime: {date: Date },
  }, {
    timestamps: true
  });
```

> With mongoose you can create '(simple) relationships' between collections, despite MongoDB is NoSQL based:
> - `{Schema.Types.ObjectId, ref: 'users'}` is connected to the 'users' collection in the same database.

## Schema
Define schema in JSON format within the `new mongooseClient.Schema`

```js
{
  username: { type: String, required: true },
  name: { type: String, required: true },
  timeStamp: { type: Date, default: new Date() },
  isOnline: {type: Boolean, default: true, required: true}
}
```
> ~~The class **mongooseClient.Schema** doesn't set any value if you define it as default **false** even with the ***required*** flag.~~ 
After rebooting the server and recreating a new user it sets the default to `false`
{.is-warning}


[Official Documentation](http://mongoosejs.com/docs/models.html)

---
# MongoDB native

```bash
```