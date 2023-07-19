---
layout: default
title: Mongo DB Introduction
parent: Mongo DB
grand_parent: Spring Boot
nav_order: 1
---
### Mongo Db [Official Link](https://www.mongodb.com/docs/atlas/)
MongoDB is a popular open-source, NoSQL document database that provides high performance, scalability, and flexibility for storing and managing structured and unstructured data. It was first released in 2009 by the company 10gen, which is now known as MongoDB Inc.

Unlike traditional relational databases, MongoDB follows a document-oriented data model. It stores data in flexible, JSON-like documents called BSON (Binary JSON), which allows for dynamic schemas and supports a wide variety of data types. This flexibility makes MongoDB well-suited for handling evolving and diverse data structures, such as those encountered in web applications and other modern software systems.

Key features of MongoDB include:
1. Scalability: MongoDB is designed to scale horizontally across multiple servers, allowing for the distribution of data and workload across a cluster of machines. This enables it to handle large amounts of data and high traffic loads.
2. High Performance: MongoDB's architecture is optimized for performance, utilizing memory-mapped files and providing automatic indexing for faster data access. It also supports replica sets and sharding, which further enhance scalability and availability.
3. Querying and Indexing: MongoDB provides a flexible and powerful query language that supports complex queries, indexing, and aggregation operations. It supports a wide range of query patterns and allows for efficient data retrieval and manipulation.
4. High Availability: MongoDB supports automatic failover through replica sets, which are groups of database instances that maintain identical copies of data. If one instance fails, another replica automatically takes over to ensure continuous availability.
5. Horizontal Data Model: MongoDB's document-oriented approach allows for easy denormalization of data, embedding related information within a single document or linking documents using references. This can simplify data access and improve performance.

MongoDB also offers various additional features and tools, including data encryption, authentication and authorization mechanisms, monitoring and management tools, and integration with popular programming languages and frameworks.

Overall, MongoDB is widely used in modern applications, including content management systems, e-commerce platforms, real-time analytics systems, and many other use cases where flexible and scalable data storage is required.

### Set up MongoDB on a Mac
To set up MongoDB on a Mac, you can follow these steps:

Step 1: Install Homebrew (Package Manager)
* Open Terminal on your Mac.
* Run the following command to install Homebrew:
```markdown
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Step 2: Install MongoDB
* In Terminal, run the following command to install MongoDB using Homebrew:
```markdown
brew install mongodb-community
```
Step 3: Create the MongoDB Data Directory
* MongoDB requires a data directory to store its database files. By default, it uses /data/db, but this directory doesn't exist by default on macOS.
* Create the directory by running the following command:
```markdown
sudo mkdir -p /data/db
```
Step 4: Set Permissions for the Data Directory
* Run the following command to set the correct permissions for the data directory:
```markdown
sudo chown -R `id -un` /data/db
```
Step 5: Start MongoDB
* Start the MongoDB server by running the following command:
```markdown
brew services start mongodb-community
```
Step 6: Verify the MongoDB Installation
* To verify that MongoDB is running correctly, open a new Terminal window and run the following command:
```markdown
mongod --version
```

### Here are some common MongoDB commands with examples:
1. use: Switch to a specific database.
    ```markdown
    use myDatabase
    ```
2. db.createCollection: Create a new collection within the current database.
    ```markdown
    db.createCollection("myCollection")
    ```
3. db.collection.insertOne: Insert a document into a collection.
    ```markdown
    db.myCollection.insertOne({ name: "John", age: 30 })
    ```
4. db.collection.insertMany: Insert multiple documents into a collection.
    ```markdown
    db.myCollection.insertMany([{ name: "John", age: 30 }, { name: "Jane", age: 25 }])
    ```
5. db.collection.find: Retrieve documents from a collection.
    ```markdown
    db.myCollection.find()
    ```
6. db.collection.findOne: Retrieve the first document that matches a query.
    ```markdown
    db.myCollection.findOne({ name: "John" })
    ```
7. db.collection.updateOne: Update a single document that matches a query.
    ```markdown
    db.myCollection.updateOne({ name: "John" }, { $set: { age: 31 } })
    ```
8. db.collection.updateMany: Update multiple documents that match a query.
    ```markdown
    db.myCollection.updateMany({ name: "John" }, { $set: { age: 31 } })
    ```
9. db.collection.deleteOne: Delete a single document that matches a query.
    ```markdown
    db.myCollection.deleteOne({ name: "John" })
    ```
10. db.collection.deleteMany: Delete multiple documents that match a query.
    ```markdown
    db.myCollection.deleteMany({ name: "John" })
    ```
11. db.collection.aggregate: Perform aggregation operations on documents.
    ```markdown
    db.myCollection.aggregate([{ $group: { _id: "$name", total: { $sum: "$age" } } }])
    ```
12. db.collection.find().sort: Sort the retrieved documents in ascending or descending order.
    ```markdown
    db.myCollection.find().sort({ age: 1 }) // ascending order
    db.myCollection.find().sort({ age: -1 }) // descending order
    ```
13. db.collection.find().limit: Limit the number of documents to retrieve.
    ```markdown
    db.myCollection.find().limit(10) // retrieve only 10 documents
    ```
14. db.collection.find().skip: Skip a specified number of documents.
    ```markdown
    db.myCollection.find().skip(5) // skip the first 5 documents
    ```
These are just a few examples of MongoDB commands. MongoDB provides a rich set of operations and query capabilities. For a comprehensive list of commands and their usage, I recommend referring to the official MongoDB documentation (https://docs.mongodb.com/manual/).    

