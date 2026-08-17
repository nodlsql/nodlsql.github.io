# Data types

The standard JSON data types are supported:
| Data type | Description | Example |
| -------- | ----------- | ------- |
| String | Text enclosed in double quotes | "hello" |
| Number | Integer or floating-point number | 42, 3.14 |
| Boolean | True or false values | true, false |
| Null | An empty value | null |
| Object | Unordered key-value pairs | {"id": 1} |
| Array | Ordered list of values | [1, 2, 3]

String constants are enclosed in single quotes when expressed in the query syntax:
```sql
SELECT * FROM dev WHERE idtag = 'joe';
```

In the result set string scalar values and json objects are returned with no embedding quotes:
```sql
SELECT vibe, title.level, title from job where vibe <> 'so so';
---
good, 5, {"level":5,"name":"rust guru"}
```

