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
CREATE DATASET job PRIMARY KEY(title.name, title.level);
CREATE DATASET dev PRIMARY KEY(idtag), RELATIONSHIP tasks(job);
```
## Alter

A dataset schema can be updated via the ALTER statement:
```sql
ALTER DATASET job DROP RELATIONSHIP tasks, ADD RELATIONSHIP errands(job);
ALTER DATASET dev ADD PRIMARY KEY(idtag), DROP INDEX idx;
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
--
CREATE DATASET job
    PRIMARY KEY(title.name, title.level);
```

To get the list of datasets:
```sql
SELECT name FROM DATASET;
--
job
dev
```