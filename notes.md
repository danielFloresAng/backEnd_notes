// CRUD //

<!--
C -> Create
R -> Read
U -> Update
D -> Delete
-->

// MONGO DB //

<!-- CRUD in Mongo -->

- db.collection_name.insertOne(doc)
  -> add a new documment to the collection

- db.collection_name.insertMany(docs)
  ->Adds severals documents to the collection(an array of documents)

- db.collection_name.findOne(opt)
  -> Return the first found document that contains the search criteria(opt)

- db.collection_name.find(opt)
  -> Return all the documents that contains the search criteria

- db.collection_name.find(opt).pretty()
  -> Shows the results of find() method more readables

<!-- ---- Methods ----  -->

- use data_base_name
  --> select de DB that we want to use

- db.collection_name.find({query})
  --> finds the documents we want in the collection

- db.createCollection('collection_name')
  --> creates new collection

- show dbs
  --> shows all the databases

- db.collection_name.insertOne({'property': "value"})
  --> adds an object

- db.collection_name.insertMany([{array_with_two_or_more_objects}])
  --> adds an array with severals objects

- db.collection_name.deleteOne({"property":"value"})
  --> delete one document in the selected collection

- db.collection_name.estimateDocumentCount()
  -> Makes an aproximate count of the documets by its metadata

- db.collection_name.countDocuments(opt)
  -> Makes a count of the documets that contains the options(opt)

- db.collection_name.updateOne({"unique_property": "value"}, {"property_to_update": "new_value"})
      --> Updates one property of the selected collection, usually we are going to use the collection ID to select the object to update.

<!-- Operators in Mongo DB -->

- $and
    syntax -> {$and:[{},{}]}

- $or
    syntax -> {$or:[{},{}]}

- $lt (les than)
    syntax -> {'propery':{$lt: "value_condition"}}

- $lte (les than or equal)
    syntax -> {'propery':{$lte: "value_condition"}}

- $gt (greater than)
    syntax -> {'propery':{$gt: "value_condition"}}

- $gte (greater than or equal)
    syntax -> {'propery':{$gte: "value_condition"}}

- $ne (not equal)
    syntax -> {'propery':{$ne: "value_condition"}}

- $eq (equal)
    syntax -> {'propery':{$eq: "value_condition"}}

<!--
//// Note: 
We cand write one or more conditions to filter elements, just need to separate them with a come ",".  

Ej.:
db.students.find({"gender": "Male", "age": {$lt:40}})
 -->


<!-- Limit, Skip and Sort -->
- .sort("name": -1)  
    -> Orders the documents in descendant or ascendent, depends of the properties selected.

- .skip(offset)
    -> Omit the numbers of the indicated documents with the offset

- .limit(num)
    -> Limits the number of the returned documents