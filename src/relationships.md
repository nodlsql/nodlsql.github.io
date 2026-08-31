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

# Relationships

Relationships provide an efficient alternative to joins. A relationship links items from a source dataset to target dataset items identified by their primary key values.

See also [dataset](dataset.md) for relationship schema definitions.

## Insert

Inserts a successor in a relationship. The values specified map to the target dataset's existing primary key segments, in the order they are declared.

For instance with a target dataset `job` set as follows:
```sql
CREATE DATASET job PRIMARY KEY(title.name, title.level);
INSERT INTO job VALUES
  '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}';
```

With a relationship defined on dataset `dev` as:
```sql
CREATE DATASET dev RELATIONSHIP tasks(job);
```

You can now insert a `job` item as a `dev` item successor through the `tasks` relationship:
```sql
INSERT INTO dev VALUES '{"idtag": "joe", "greeting": "hi!"}';
INSERT INTO dev.tasks VALUES ('rust guru', 5) WHERE idtag = 'joe';
```

Many-to-many relationships are supported. In this example a `dev` item can have multiple `tasks` successors. A `job` item can have multiple `dev` item predecessors.

## Delete

To delete the relationship successor from the previous example:
```sql
DELETE FROM dev.tasks VALUES('rust guru', 5) WHERE idtag = 'joe';
```

## Relationship navigation

You can filter items via direct or inverse relationship navigation.
```sql
SELECT * FROM dev WHERE tasks.vibe = 'good';
SELECT * FROM job WHERE INVERSE(dev.tasks).idtag = 'joe';
```

The same expressions can be used in projection:
```sql
SELECT idtag, tasks.* FROM dev WHERE greeting = 'hi!';
```

The `SELECT *` projection provides a relationship summary.
With data from the previous examples:
```sql
SELECT * FROM dev;
```
Select result:
```json
{"greeting":"hi!","idtag":"joe","tasks":"rust guru 5"}
```

The same projection without summary:
```sql
SELECT d FROM dev d;
```
Select result:
```json
{"greeting":"hi!","idtag":"joe"}
```
