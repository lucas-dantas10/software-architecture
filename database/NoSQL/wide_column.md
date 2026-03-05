# Wide Column

## What is?

These databases store data in columns rather than rows, organizing them into column families (groups of columns sharing 
attributes). Each row can have a variable number of columns with different data types.

## Focus

Organizes data into columns, focusing on high-speed writing and scalability.

## Use Cases

- Useful for storing large amounts of data within a single column, which helps reduce disk resources and speeds 
up the retrieval of specific information.
- AWS Example: Amazon Keyspaces.

## Example

### Create
```sql
INSERT INTO usuarios (id, nome, idade) VALUES (1, 'Ana', 28);
```

### Read
```sql
SELECT * FROM usuarios WHERE id = 1;
```

### Update
```sql
UPDATE usuarios SET idade = 29 WHERE id = 1;
```

### Delete
```sql
DELETE FROM usuarios WHERE id = 1;
```
