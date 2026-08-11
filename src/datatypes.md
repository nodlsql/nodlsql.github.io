# Data types

The standard JSON data types are supported:
| Data type | Description | Example |
| -------- | ----------- | ------- |
| String | Text enclosed in single quotes | 'hello' |
| Number | Integer or floating-point number | 42, 3.14 |
| Boolean | True or false values | true, false |
| Null | An empty value | null |
| Object | Unordered key-value pairs | {"id": 1} |
| Array | Ordered list of values | [1, 2, 3]

Result set string scalar values and json elements don't have embedding quotes:
```sql
SELECT vibe, title from job where vibe <> 'so so';
---
good, {"level":5,"name":"rust guru"}
```

