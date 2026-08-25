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

# Dataset

Datasets hold collections of json objects. A dataset can be created with primary key indexes, unique/non-unique indexes and relationships with other datasets.

## Create

To create a dataset:
```sql
CREATE DATASET job;
```

Indexes can be multi-segments and support path traversal, for instance the `title.name` path for items like:
```json
{
  "title": {
    "name": "rust guru",
    ...
  }
}
```

Index definition examples:
```sql
CREATE DATASET pkds PRIMARY KEY(a.b, c);
CREATE DATASET ixds UNIQUE INDEX uix(a), INDEX dupix(b);
```

Relationships are based on the primary key of the target dataset.

The following statements create the `tasks` relationship between the source dataset `dev` and the target dataset `job`, based on the `job` primary key:
```sql
CREATE DATASET job
  PRIMARY KEY(title.name, title.level)
  INDEX idx(vibe);

CREATE DATASET dev
  PRIMARY KEY(idtag),
  INDEX idx(greeting),
  RELATIONSHIP errands(job);
```
## Alter

A dataset schema can be updated via the ALTER statement:
```sql
ALTER DATASET dev
  DROP RELATIONSHIP errands,
  ADD RELATIONSHIP tasks(job),
  DROP PRIMARY KEY, DROP INDEX idx;
```

## Drop

Deletes a dataset and associated indexes and relationships.

Example:
```sql
DROP DATASET dev;
```

## Describe

Describes a dataset and associated indexes, relationships.

Example:
```sql
DESCRIBE DATASET job;
```
Describe result:
```sql
CREATE DATASET job
    PRIMARY KEY(title.name, title.level);
```

To get the list of datasets:
```sql
SELECT name FROM DATASET;
```
Select result:
```
job
dev
```
