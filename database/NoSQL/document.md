# Document

## What is?

Data is stored in documents, which are typically nested structures of keys and values (like JSON, BSON, or XML). 
Unlike relational databases, there is no single schema enforced upon all documents.

## Focus

Stores data in JSON/BSON. Focuses on flexibility.

## Use Cases

- Ideal for application code that uses object models, allowing developers to transfer code objects directly into 
documents. It is also great for full-text search and secondary indexes.
- AWS Example: Amazon DocumentDB(with MongoDB compatibility).

## Example

### Create
```
db.usuarios.insertOne({nome: "Ana", idade: 28})
```

### Read
```
db.usuarios.find({nome: "Ana"})
```

### Update
```
db.usuarios.updateOne({nome: "Ana"}, {$set: {idade: 29}})
```

### Delete
```
 db.usuarios.deleteOne({nome: "Ana"})
```
