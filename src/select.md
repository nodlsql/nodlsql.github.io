# Select

The `SELECT` statement supports joins, relationship navigation, path expressions and jsonpath.

## Select list

The `FROM` clause specifies the list of datasets to query. Multiple datasets, aliases can be specified for joining between datasets.

For instance for a `dev` item with a `wants` element looking for a new job title:
```sql
INSERT INTO job VALUES '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}';
INSERT INTO dev VALUES '{"greeting":"hi!","idtag":"joe","wants":"rust guru"}';
SELECT j.title, d.idtag FROM job j, dev d WHERE d.wants = j.title.name;
--
{"level":5,"name":"rust guru"}, joe
```

## Predicate evaluation

The `WHERE` clause predicates filter the result set. Path expressions like a, a.b, a.b.c can be used, or jsonpath.
Predicates are joined with the `AND` operator that returns an item if all conditions evaluate to true.

```sql
SELECT * FROM job WHERE title.level IN (2, 3) AND vibe NOT LIKE '%so';
```

The following comparison operators are supported:
| Operator | Descripion | Example |
| -------- | ---------- | ------- |
|`=`, `<>`, `>=`, `<=`, `<, >` | equal, not equal, ge, le, gt, lt | `WHERE i <> 1` |
|`IN`, `NOT IN` | Scalar value included/not included in value list | `WHERE i NOT IN(1, 3, 5)` |
|`IS NULL`, `IS NOT NULL` | Field doesn't/does exist. To distinguish from `i = null` comparison against json value `null` | `WHERE i IS NULL` |
|`LIKE`, `NOT LIKE` | Field matches/doesn't match a pattern where `%` represents zero, one or multiple characters, `_` represents a single character | `WHERE a LIKE 'ther%'` | 
|`REGEXP`, `NOT REGEXP` | Field matches/doesn't match a [regular expression pattern](https://en.wikipedia.org/wiki/Regular_expression) pattern | `WHERE a REGEXP '^ther.*$'` | 

The arithmetic operators `+`, `-`, `*`, `/` are supported for addition, substraction, multiplication and division.

## Projection

Single result or comma separated projection results are supported.

Example:
```sql
SELECT 1 + (1.50 * 2);
SELECT title, vibe FROM job;
```