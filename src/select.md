<!--
Copyright 2026 No Despondency Labs.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# Select

The `SELECT` statement supports joins, relationship navigation, path expressions and JSONPath.

## Select list

The `FROM` clause specifies the datasets to query. Dataset aliases can be specified for joining between datasets.

For example, for a `dev` item with a `wants` element looking for a new job title:
```sql
INSERT INTO job VALUES '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}';
INSERT INTO dev VALUES '{"greeting":"hi!","idtag":"joe","wants":"rust guru"}';
SELECT j.title, d.idtag FROM job j, dev d WHERE d.wants = j.title.name;
```
Select result:
```json
{"level":5,"name":"rust guru"}, joe
```

## Predicate evaluation

The `WHERE` clause filters the result set using predicates. You can use path expressions like `a`, `a.b`, `a.b.c`, or JSONPath.
Predicates joined with the `AND` operator return the items for which all conditions evaluate to true.

```sql
SELECT * FROM job WHERE title.level IN (2, 3, 5) AND vibe NOT LIKE 'so%';
```

The following comparison operators are supported:
| Operator | Description | Example |
| -------- | ---------- | ------- |
|`=`, `<>`, `>=`, `<=`, `<, >` | equal, not equal, ge, le, gt, lt | `WHERE i <> 1` |
|`IN`, `NOT IN` | Scalar value included/not included in value list | `WHERE i NOT IN(1, 3, 5)` |
|`IS NULL`, `IS NOT NULL` | Field doesn't/does exist. To distinguish from `i = null` comparison against JSON value `null` | `WHERE i IS NULL` |
|`LIKE`, `NOT LIKE` | Field matches/doesn't match a pattern where `%` represents zero, one or multiple characters, `_` represents a single character | `WHERE a LIKE 'ther%'` | 
|`REGEXP`, `NOT REGEXP` | Field matches/doesn't match a [regular expression pattern](https://en.wikipedia.org/wiki/Regular_expression) pattern | `WHERE a REGEXP '^ther.*$'` | 


The arithmetic operators `+`, `-`, `*`, `/` are supported for addition, subtraction, multiplication and division. Parentheses can be used to override standard operator precedence.

## Projection

Comma-separated projection results are supported.

Example:
```sql
SELECT 1 + (1.50 * 2), 3.0/4;
SELECT title, vibe FROM job;
```
