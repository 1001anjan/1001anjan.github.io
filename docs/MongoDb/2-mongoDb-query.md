---
layout: default
title: MongoDB Query Practice
parent: Mongo DB
nav_order: 2
---
### MongoDB Query Examples on Products
1. Create Product 
    * `insertOne()`
      ```markdown
      db.products.insertOne({
      name: "Product Name",
      description: "Product description",
      price: 19.99,
      category: "Electronics",
      tags: ["smartphone", "android"],
      createdAt: new Date()
      })
       ```
    * `insertMany()`
      ```markdown
      db.products.insertMany([
      {
      name: "Product 1",
      description: "Product 1 description",
      price: 9.99,
      category: "Clothing",
      tags: ["t-shirt", "casual"],
      createdAt: new Date()
      },
      {
      name: "Product 2",
      description: "Product 2 description",
      price: 29.99,
      category: "Electronics",
      tags: ["headphones", "wireless"],
      createdAt: new Date()
      }
      ])
       ```
2. List Documents
    * `find()` method
      ```markdown
      db.products.find()
      ```
      ```markdown
      db.products.find({ category: "Electronics" })
      ```  
      ```markdown
      db.products.find({ name: {$regex: /ASUS/i}})
      ```
      `{ name: { $regex: /keyword/i } }`: Specifies the search criteria. The "name" field is matched using the $regex operator with the regex pattern `/keyword/i`. The i flag makes the regex case-insensitive, so it will match "keyword", "KeyWord", "KEYWORD", etc.
      ```markdown
      db.products.find({price : { $gt : 10}})
      ```
      ```markdown
      db.products.find({price : { $gte : 10}})
      ```
      ```markdown
      db.products.find({price : { $lte : 10}})
      ```
      ```markdown
      db.products.find({price : { $lt : 10}})
      ```
      ```markdown
      db.products.find({price : { $gt: 2, $lte : 10}})
      ```
      ```markdown
      db.products.find({ category: { $in: ["Electronics", "Clothing"] } }) 
      ```
      ```markdown
      db.products.find({ createdAt : {$lt : new Date()}})
      ```
      ```markdown
      db.products.find({ createdAt : {$lt : new Date("2023-07-19")}})
      ```
      ```markdown
      db.products.find({ $and: [{createdAt :{$lt : new Date("2023-07-19")}}, {createdAt: {$gt: new Date("2021-09-12")}}]})
      ```
      The `$and` operator combines the two conditions.
      ```markdown
      db.products.find({ $or: [{createdAt :{$lt : new Date("2023-07-19")}}, {createdAt: {$gt: new Date("2021-09-12")}}]})
      ```
      The date format should match the format stored in your database.
      MongoDB provides various comparison operators like `$gte` (greater than or equal to), `$lte` (less than or equal to), `$ne` (not equal to), etc.
      ```markdown
      db.products.find().sort({ price: 1 }) 
      ```
      Sorting product in ascending order price
      ```markdown
      db.products.find().sort({ price: -1 }) 
      ```
      Sorting product in descending order price
      ```markdown
      // Find products sorted by price in ascending order and limit the results to 5
      db.products.find().sort({ price: 1 }).limit(5);
      ```
3. Update Operation
    ```markdown
     // Update the price of a product with a specific _id
     db.products.updateOne(
       { _id: ObjectId("6123456789abcdef0123456") },
       { $set: { price: 29.99 } }
     );
    ```
   ```markdown
    // Update the price and quantity of a product with a specific _id
    db.products.updateOne(
        { _id: ObjectId("6123456789abcdef0123456") },
        { $set: { price: 29.99, quantity: 100 } }
    );
   ```
   ```markdown
   db.products.updateMany({ price: {$gt: 50}}, {$set: {category: "Premium"}})
   ```
   ### Increment a Numeric Field:
   ```markdown
   // Increment the quantity of a product by 10
   db.products.updateOne(
     { _id: ObjectId("6123456789abcdef0123456") },
     { $inc: { quantity: 10 } }
   );
   ```
   In this example, we use the `$inc` operator to increment the value of a numeric field (quantity) by 10. The document to be updated is identified using the `_id` field.
   ### Update an Array Field:
   ```markdown
   // Add a new tag to the tags array of a product
   db.products.updateOne(
    { _id: ObjectId("6123456789abcdef0123456") },
    { $push: { tags: "newtag" } }
   );
   ```
   We use the `$push` operator to add a new tag to the existing tags array of a product document. The document to be updated is identified using the `_id` field.
   ```markdown
   // Remove a specific tag from the tags array of a product
   db.products.updateOne(
   { _id: ObjectId("6123456789abcdef0123456") },
   { $pull: { tags: "tagToRemove" } }
   );
   ```
   In this example, we use the `$pull` operator to remove the element "tagToRemove" from the "tags" array field of a product document.
   To remove all occurrences of "tagToRemove" from the array, you can use `$pullAll` instead of `$pull` with an array of values to remove.
   ### Update Nested Fields:
   ```markdown
    // Update the address fields of a user document
   db.users.updateOne(
     { _id: ObjectId("6123456789abcdef0123456") },
     { $set: { "address.city": "New City", "address.zip": "12345" } }
   );
   ```
   We use the `$unset` operator to remove the discount field from a product document. The field is specified as an empty string value within the `$unset` operator. 
   ```markdown
   // Update a product document with various operations
   db.products.updateOne(
     { _id: ObjectId("6123456789abcdef0123456") },
     {
       $set: {
           name: "New Product Name",
           price: 39.99,
           category: "Electronics",
       },
       $push: { tags: "newtag" },
       $inc: { quantity: 10 },
       $unset: { discount: "" }
     }
   );
   ```
4. Delete Operation
   ```markdown
   // Delete a product document by its _id
    db.products.deleteOne({ _id: ObjectId("6123456789abcdef0123456") });
   ```
   ```markdown
   // Delete all products with a price less than 10
    db.products.deleteMany({ price: { $lt: 10 } });
   ```
   ```markdown
   // Delete all products with a certain category
   db.products.deleteMany({ category: "Electronics" });
   ```
   ```markdown
   // Delete all documents in the "products" collection
    db.products.deleteMany({});
   ```
   ```markdown
   // Delete products with a price less than 10 and a quantity of 0
    db.products.deleteMany({
     $and: [
         { price: { $lt: 10 } },
         { quantity: 0 }
        ]
    });
   ```
5. Aggregation Operation:
   Here are some common aggregation stages and operators that can be used in aggregation queries on a "products" collection:
   * Grouping:
      * `$group`: Groups documents based on a specified key and performs aggregation operations on grouped data.
      * `$sortByCount`: Groups documents and sorts them by the count of occurrences.
   * Filtering:
      * `$match`: Filters documents based on specified criteria.
   * Projection:
      * `$project`: Reshapes the documents by including or excluding specific fields.
      * `$addFields`: Adds new fields to the documents.
   * Sorting:
      * `$sort`: Sorts the documents based on specified fields.
   * Aggregation:
      * `$sum`: Calculates the sum of numeric fields.
      * `$avg`: Calculates the average of numeric fields.
      * `$min`: Finds the minimum value of a field.
      * `$max`: Finds the maximum value of a field.
      * `$count`: Counts the number of documents in a group or field.
      * `$first`: Returns the first value in a group.
      * `$last`: Returns the last value in a group.
   * Array Operations:
      * `$unwind`: Breaks down an array field into separate documents.
      * `$addToSet`: Adds unique values to an array field.
   * Limiting and Skipping:
      * `$limit`: Limits the number of documents in the result set.
      * `$skip`: Skips a specified number of documents in the result set.

# Here's an example of an aggregation query using only the `$group` stage on a "products" collection:
```markdown
db.products.aggregate([
  {
    $group: {
      _id: "$category",
      totalProducts: { $sum: 1 },
      averagePrice: { $avg: "$price" },
      maxPrice: { $max: "$price" },
      minPrice: { $min: "$price" }
    }
  }
]);
```
* `$sum`: 1: Calculates the total number of products in each category.
* `$avg`: "$price": Calculates the average price of products in each category.
* `$max`: "$price": Finds the maximum price of products in each category.
* `$min`: "$price": Finds the minimum price of products in each category.

### Here's an example of an aggregation query using the `$sortByCount` operator on a "products" collection:
```markdown
db.products.aggregate([
  {
    $sortByCount: "$category"
  }
]);
```
We use the `$sortByCount` operator to group and sort the documents in the "products" collection based on the "category" field. The `$sortByCount` operator is a shorthand for the combination of `$group` and `$sort` stages, where it groups the documents by the specified field and sorts them by the count of occurrences in descending order.

````markdown
db.products.aggregate([
  {
    $match: { price: { $gte: 10 } }
  },
  {
    $group: {
      _id: "$category",
      totalProducts: { $sum: 1 },
      averagePrice: { $avg: "$price" },
    }
  },
  {
    $sort: { totalProducts: -1 }
  },
  {
    $limit: 5
  }
]);
````
In this example, the aggregation pipeline performs the following steps:

* `$match`: Filters the documents to include only those with a price greater than or equal to 10.
* `$group`: Groups the filtered documents by the "category" field and calculates the total number of products in each category (`totalProducts`) and the average price of products in each category (`averagePrice`).
* `$sort`: Sorts the grouped documents in descending order based on the "totalProducts" field.
* `$limit`: Limits the number of sorted documents to 5.

```code 
import org.springframework.data.mongodb.core.aggregation.Aggregation;
import org.springframework.data.mongodb.core.aggregation.AggregationResults;
import org.springframework.data.mongodb.core.MongoTemplate;

// ...

@Autowired
private MongoTemplate mongoTemplate;

// ...

Aggregation aggregation = Aggregation.newAggregation(
        Aggregation.match(Criteria.where("price").gte(10)),
        Aggregation.group("category")
                .sum(1).as("totalProducts")
                .avg("price").as("averagePrice"),
        Aggregation.sort(Sort.Direction.DESC, "totalProducts"),
        Aggregation.limit(5)
);

AggregationResults<Document> results = mongoTemplate.aggregate(
        aggregation, "products", Document.class);

List<Document> output = results.getMappedResults();
```

### Here's an example of an aggregation query using the `$project` and `$addFields` stages on the "products" collection:
```markdown
db.products.aggregate([
  {
    $project: {
      _id: 0,
      productName: "$name",
      discountedPrice: { $subtract: ["$price", "$discount"] }
    }
  },
  {
    $addFields: {
      isExpensive: { $cond: { if: { $gte: ["$price", 100] }, then: true, else: false } }
    }
  }
]);
```
In this example, we use the `$project` stage to reshape the documents by including or excluding specific fields. The `$project` stage is used to project the following fields:

* `productName`: Renames the existing name field as `productName`.
* `discountedPrice`: Calculates the discounted price by subtracting the discount value from the price field.
Next, we use the `$addFields` stage to add new fields to the documents. The `$addFields` stage is used to add the following field:

* `isExpensive`: Uses the `$cond` operator to conditionally assign a value (`true` or `false`) based on whether the price is greater than or equal to 100.

### Here's an example of an aggregation query using the `$unwind` and `$addToSet` operators on the "products" collection:
```markdown
db.products.aggregate([
  {
    $unwind: "$tags"
  },
  {
    $group: {
      _id: null,
      uniqueTags: { $addToSet: "$tags" }
    }
  }
]);
```
We use the `$unwind` stage to break down the tags array field into separate documents, creating a new document for each element in the array.
Next, we use the `$addToSet` stage to add unique tags to a new field called uniqueTags. The `$addToSet` operator ensures that only unique values are added to the set, eliminating any duplicate tags.
we use the `$group` stage with the `_id` set to null. This effectively groups all documents into a single group. Within the `$group` stage, we utilize the `$addToSet` operator to create an array of unique tags from the unwound tags field.

### Here's an example of an aggregation query using the `$limit` and `$skip` operators on the "products" collection:
```markdown
db.products.aggregate([
  {
    $sort: { price: -1 }
  },
  {
    $skip: 10
  },
  {
    $limit: 5
  }
]);
```
In this example, we first use the `$sort` stage to sort the documents in descending order based on the "price" field. The `-1` value indicates descending order.

Then, we use the `$skip` stage to skip the first 10 documents in the sorted order. This means we are skipping the highest-priced products.

Finally, we use the `$limit` stage to limit the number of documents returned to 5. This ensures that only 5 products with the highest prices, after skipping the initial 10, are included in the result set.

### Query on multiple collections
To query multiple collections in MongoDB, we can use the `$lookup` stage in the aggregation pipeline. The `$lookup` stage allows you to perform a left outer join between two collections based on a common field.

Here's an example of how to write a query that involves multiple collections:

We have three collections: "customers", "orders", and "payments". We want to retrieve customer information along with their corresponding orders and payments.

```markdown
db.customers.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "customerId",
      as: "customerOrders"
    }
  },
  {
    $lookup: {
      from: "payments",
      localField: "_id",
      foreignField: "customerId",
      as: "customerPayments"
    }
  },
  {
    $project: {
      _id: 1,
      name: 1,
      orders: "$customerOrders",
      payments: "$customerPayments"
    }
  }
]);
```
* The first `$lookup` stage performs a left outer join between the "customers" collection and the "orders" collection. It matches documents based on the `_id` field in the "customers" collection and the `customerId` field in the "orders" collection. The matched documents from the "orders" collection are added as an array field called "customerOrders" in the resulting documents.
* The second `$lookup` stage performs a left outer join between the "customers" collection and the "payments" collection. It matches documents based on the `_id` field in the "customers" collection and the `customerId` field in the "payments" collection. The matched documents from the "payments" collection are added as an array field called "customerPayments" in the resulting documents.
* The `$project` stage reshapes the documents to include specific fields, renaming them if needed. Here, we select the `_id` and `name` fields from the "customers" collection and assign the "customerOrders" and "customerPayments" arrays to the "orders" and "payments" fields, respectively.

```code
import org.springframework.data.mongodb.core.aggregation.Aggregation;
import org.springframework.data.mongodb.core.aggregation.AggregationResults;
import org.springframework.data.mongodb.core.MongoTemplate;

// ...

@Autowired
private MongoTemplate mongoTemplate;

// ...

Aggregation aggregation = Aggregation.newAggregation(
        Aggregation.lookup("orders", "_id", "customerId", "customerOrders"),
        Aggregation.lookup("payments", "_id", "customerId", "customerPayments"),
        Aggregation.project("_id", "name")
                .and("customerOrders").as("orders")
                .and("customerPayments").as("payments")
);

AggregationResults<Document> results = mongoTemplate.aggregate(
        aggregation, "customers", Document.class);

List<Document> output = results.getMappedResults();
```

### In MongoDB, there is no direct support for a right outer join as provided in traditional relational databases.
However, we can achieve a similar result using the `$lookup` stage and subsequent stages in the aggregation pipeline.

Let's assume you have two collections: "orders" and "customers" that you want to join based on a common field, such as "customerId".

Here's an example of how you can perform a right outer join-like operation using the `$lookup` stage and subsequent stages:

```markdown
db.customers.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "customerId",
      as: "orders"
    }
  },
  {
    $unwind: {
      path: "$orders",
      preserveNullAndEmptyArrays: true
    }
  },
  {
    $project: {
      _id: 1,
      name: 1,
      orderNumber: "$orders.orderNumber",
      orderDate: "$orders.orderDate"
    }
  }
]);
```
In this example, we perform a right outer join-like operation between the "customers" and "orders" collections based on the common field "customerId". Here's how it works:

* The `$lookup` stage joins the "orders" collection with the "customers" collection, matching documents based on the `_id` field in the "customers" collection and the `customerId` field in the "orders" collection. The matched documents from the "orders" collection are added as an array field called "orders" in the resulting documents.
* The `$unwind` stage deconstructs the "orders" array, creating a separate document for each element. The `preserveNullAndEmptyArrays`: true option ensures that documents with no matching orders are also included, resulting in a right outer join-like behavior.
* The `$project` stage reshapes the documents to include specific fields, renaming them if needed. Here, we select the `_id` and `name` fields from the "customers" collection and the "orderNumber" and "orderDate" fields from the "orders" array.
* When we use `{ name: 1 }` in the `$project` stage, it means that you want to include the name field in the output documents, retaining its original value.
```markdown
db.customers.aggregate([
  {
    $project: {
      _id: 0,
      name: 1
    }
  }
]);
```
In this example, the `$project` stage is used to reshape the documents. It includes only the name field while excluding the `_id` field using `{ _id: 0 }`. The resulting aggregation output will contain documents with only the name field and the `_id` field will be omitted.

### Here's an example of a complex query that involves multiple collections and uses various stages in the aggregation pipeline:

Assume we have three collections: "customers", "orders", and "products". We want to retrieve information about customers along with their total order count and the highest-priced product they have purchased.

```markdown
db.customers.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "customerId",
      as: "customerOrders"
    }
  },
  {
    $unwind: "$customerOrders"
  },
  {
    $lookup: {
      from: "products",
      localField: "customerOrders.productId",
      foreignField: "_id",
      as: "productInfo"
    }
  },
  {
    $group: {
      _id: "$_id",
      name: { $first: "$name" },
      orderCount: { $sum: 1 },
      maxPrice: { $max: "$productInfo.price" }
    }
  },
  {
    $sort: { orderCount: -1 }
  },
  {
    $limit: 5
  }
]);
```
In this example, we perform the following stages in the aggregation pipeline:

* `$lookup`: Joins the "customers" collection with the "orders" collection, matching documents based on the `_id` field in the "customers" collection and the `customerId` field in the "orders" collection. The matched documents from the "orders" collection are added as an array field called "customerOrders" in the resulting documents.
* `$unwind`: Deconstructs the "customerOrders" array, creating a separate document for each order.
* Another `$lookup`: Joins the resulting documents with the "products" collection, matching based on the "productId" field in the "customerOrders" array and the `_id` field in the "products" collection. The matched documents from the "products" collection are added as an array field called "productInfo" in the resulting documents.
* `$group`: Groups the documents by the `_id` (customer's `_id`) and calculates the total order count (`orderCount`) using `$sum`, retains the customer's name (`name`) using `$first`, and finds the highest-priced product (`maxPrice`) using `$max`.
* `$sort`: Sorts the documents in descending order based on the "orderCount" field.
* `$limit`: Limits the output to the top 5 documents with the highest order count.


### Implementation in Code
```code
import org.springframework.data.mongodb.core.aggregation.Aggregation;
import org.springframework.data.mongodb.core.aggregation.AggregationResults;
import org.springframework.data.mongodb.core.MongoTemplate;

// ...

@Autowired
private MongoTemplate mongoTemplate;

// ...

Aggregation aggregation = Aggregation.newAggregation(
        Aggregation.lookup("orders", "_id", "customerId", "customerOrders"),
        Aggregation.unwind("customerOrders"),
        Aggregation.lookup("products", "customerOrders.productId", "_id", "productInfo"),
        Aggregation.group("_id")
                .first("name").as("name")
                .sum(1).as("orderCount")
                .max("productInfo.price").as("maxPrice"),
        Aggregation.sort(Sort.Direction.DESC, "orderCount"),
        Aggregation.limit(5)
);

AggregationResults<Document> results = mongoTemplate.aggregate(
        aggregation, "customers", Document.class);

List<Document> output = results.getMappedResults();

```











   
      
  