# MongoDB Essentials.

*Understand the Basics of MongoDB*

## 1. Introduction

It is a noSQL database, it uses documents instead of tables as in SQL.

* Data is structure using BSON similar structure like JSON.
* Its NoSQL or non-relational, therefore no joins but you can use references.

### 1.1 Advantages

* Easy to change scheme
* Compared to SQL, noSQL is scalable and better performer.
* Object oriented
* Agile dev is easy as easy accomodate rapidly changing structured, semi-structured and unstructured data easily.

    *eg: Upadate user scheme whenever required*
* Cluster Scale. Distributing the database across 100+ nodes, often in multiple data centers

* Performance Scale. Sustaining 100,000+ database read and writes per second while maintaining strict latency SLAs

* Data Scale. Storing 1 billion+ documents in the database


### 1.2 Types

* **Document databases** pair each key with a complex data structure known as a document. Documents can contain many different key-value pairs, or key-array pairs, or even nested documents.

* **Graph stores** are used to store information about networks of data, such as social connections. Graph stores include Neo4J and Giraph.

* **Key-value stores** are the simplest NoSQL databases. Every single item in the database is stored as an attribute name (or 'key'), together with its value. Examples of key-value stores are Riak and Berkeley DB. Some key-value stores, such as Redis, allow each value to have a type, such as 'integer', which adds functionality.

* **Wide-column stores** such as Cassandra and HBase are optimized for queries over large datasets, and store columns of data together, instead of rows.

### 1.3 Units of storage

**Docuemnt :** Basic unit of data in mongoDB. One record in mongoDB, represented in BSON, looks similar to JSON with key & value.

```js
    {
        field1: value1,
        field2: value2,
        field3: value3,
        fieldN: valueN
    }
```

**Collection :** Grouping of MongoDB documents of similar or related purpose.

```js
    {
        field1: value1,
        fieldN: valueN
    }
    {
        field1: value1,
        fieldN: valueN
    }
```

## 2. Installation

**Installtion on ubuntu 18.**.**

`sudo apt-get install mongodb`

`service mongodb status`

**Accessing MongoDB shell**

terminal 1 `$mongod`

terminal 2 `$mongo`

## 3. Using Mongo Shell

### 3.1 Operations.

* Show Databases: `show dbs`
* Create or start using databases: `use database_name`
* Accessing uses `db. <....>`
* Creating collection `db.createCollection("cars")` result would be `{ "ok" : 1 }`
* Listing Collections `show collections`
* Inserting dta into collections:
    ```json
        db.cars.insert({
            name: 'honda',
            make: 'accord',
            year: '1988'
        })
    ```
    Result: `WriteResult({ "nInserted" : 1 })`
* Finding data `db.cars.find()`
* Formating output: `db.cars.find().pretty()`

***Input might be in JSON (with no key quotes), it'll be stored in BSON format in database***

* Update:
    ```json
    db.cars.update({
        name: 'honda'
        },
        {
            $set:{
                name:'ford'
            }
        })
    ```
    Output: `WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })`

* Update collection:
    ```json
    db.cars.update({
        name: 'ford'
        },
        {
            $set:{
                transmission:'automatic'
            }
        },
        {
            $upsert:true
        })
    ```
    Output: `WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })`

* Remove: Removes matching collections or all.

    `db.cars.remove({ name: 'ford' })`

    Output: `WriteResult({ "nRemoved" : 1 })`

* Autogenerate inputs: (Because it's a javascript interpretor)

    ```js
    for(var i=0; i<10; i++){
        db.cars.insert({wheels: i})
    }
    ```
    Output:
    ```json
    db.cars.find().pretty()

    { "_id" : ObjectId("5c7fbf82e3e307d4797836c6"), "wheels" : 0 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836c7"), "wheels" : 1 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836c8"), "wheels" : 2 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836c9"), "wheels" : 3 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836ca"), "wheels" : 4 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836cb"), "wheels" : 5 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836cc"), "wheels" : 6 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836cd"), "wheels" : 7 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836ce"), "wheels" : 8 }
    { "_id" : ObjectId("5c7fbf82e3e307d4797836cf"), "wheels" : 9 }

    ```
### 3.2 Datatypes allowed

1. String 

    `{name: "Ramesh"}`

2. Number 

    `{count: 2}`

3. Date 

    `{time: ISODate("...")}`

4. Array

    `{tags: ["t1","t2"]}`

5. Boolean

    `{pub: true}`

5. ObjectID
    `{_creator_: "1212"}`

6. Buffer -> Video/Images

7. Mixed -> Combined

### 3.3 Querying Database

**Find**

* `db.cars.find({})`
* `db.cars.find({'name':'accord'})`
* `db.cars.find({units: {$gt:6} })`
* `db.cars.find({units: {$lt:6} })`
* `db.cars.find({units: {$in:['val1','val2']} })`

**Sort & Limit**

* `db.cars.find({}).sort({name:1}).limit(2)`
* `db.cars.find({}).sort({name:-1}).limit(2)`



#### Things to read
* Redis DB
* In memory vs on disk DB systems
* Redis cache DB
