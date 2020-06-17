---
title: MongoDB
description: 
published: true
date: 2020-06-16T19:15:46.258Z
tags: 
editor: undefined
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
You can search all documents or on exact key/values pairs.
If you want to search all the values you have to create an Index.
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
### Create an Index
```js
// connect to a Database
use database_name;
// this will index all values within a collection
db.collection_name.createIndex( { "$**" : 1 } );
```
---
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

> With mongoose you can create '(simple) relationships' between 'Collections', despite MongoDB is NoSQL based:
> - `{Schema.Types.ObjectId, ref: 'users'}` is connected to another collection 'users' in the same database.

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
> ~~the class `mongooseClient.Schema` doesn't set any value if you define it as default `false` even with the ***required*** flag.~~ 
After rebooting the server and recreating a new user it sets the default to `false`
{.is-warning}


[Official Documentation](http://mongoosejs.com/docs/models.html)

---
# MongoDB native