---
title: Indexing in MongoDB
author: Anudeep Kakkireni
date: 2022-11-08 17:47:00 +0530
categories: [Indexing,MongoDB]
description: In this you'll be learning what is indexing and how it works.
tags: [indexing,commands,mongodb,mongo]
---
## Overview
MongoDB uses indexing in order to make the query processing more efficient. Without index whole collection must be scanned (COLLSCAN). Indexes are special data structures that stores some information related to the documents such that it becomes easy for MongoDB to find the right data file. 
- Index stores sorted field values.
- If appropriate index exists, MongoDB performs only index scan (IXSCAN). 
- Indexes are stored as B-Tree structure. Indexes are stored in along with the collection data in the data directory of the MongoDB.

## Index Creation Process
For example, if you created an index for age field, then each index node contains field value and record pointer (points to corresponding document) that helps us to access document efficiently. Indexes and documents are mapped as shown in below figure:

![Desktop View](/assets/img/post_images/Index_creation_process.jpg)

## Default _id index
- {_id: 1 } is default index in each MongoDB collection.
- Name of this index is id.
- Default id index is unique.

## Creating an Index
```
db.collection.createIndex( { <keyname>: [-1 | 1] }, <options>)
```
Example:
```
db.persons.createIndex( { age: 1 } )
```
## Index Creating options:
- Create index in the background. Other operations (aggregate, find) will not be blocked
```
{ background: true }
```
- Create unique index
```
{ unique: true }
```
- Specify custom name for the index
```
{ name: "<indexName>"}
```

## Get all indexes
- Returns current indexes for certain collection
```
db.‹collectionName›.getIndexes()
```

## Analyse query performance
Returns information about the query
```
db.<collectionName›.explain().<method>
```
Returns stats about the query
```
db.‹collectionName›.explain("executionStats").‹method>
```

## Delete indexes
Deletes certain index
```
db.collection.dropIndex( { ‹fieldName›: 1 } )
```
Delete all indexes:
```
db.collection.dropIndexes()
```
Example:
```
db.persons.dropIndex( { age: 1 } )
```
