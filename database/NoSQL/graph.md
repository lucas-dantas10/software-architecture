# Graph

## What is?

Designed to store and query highly connected data. Data is modeled as entities (nodes/vertices) and the relationships 
between them (edges).

## Focus

Focused on relationships between data.

## Use Cases

- Best for scenarios where relationships carry significant meaning, such as social networks 
(e.g., finding "friends of friends") or pattern matching across complex data structures.
- AWS Example: Amazon Neptune.


## Example

### Create
```sql
CREATE (n:Usuario {nome: 'Ana', idade: 28})
```

### Read
```sql
MATCH (n:Usuario {nome: 'Ana'}) RETURN n
```

### Update
```sql
MATCH (n:Usuario {nome: 'Ana'}) SET n.idade = 29
```

### Delete
```sql
MATCH (n:Usuario {nome: 'Ana'}) DELETE n

```
