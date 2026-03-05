# Key Value Pair

## What is?

This type of database stores data as a collection of key-value pairs, where each item is identified by a 
unique key. The value associated with the key can be anything, such as a string, number, or complex object.

## Focus

Stores single pairs, ideal for caching and sessions.

## Use Cases

- use case: It is optimized for applications requiring low latency and large data volumes where data is retrieved 
by a primary identifier.
- AWS Example: Amazon DynamoDB.

## Example

### Create
```redis
SET user:100 '{"nome": "Ana", "idade": 28}'
```

### Read
```redis
GET user:100
```

### Update
```redis
SET user:100 '{"nome": "Ana", "idade": 29}'
```

### Delete
```redis
DEL user:100
```