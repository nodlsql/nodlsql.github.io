# Relationships

Relationship are an efficient alternative to joins. A relationship binds items from a source dataset to target dataset items identified by their primary key values.
See also [dataset](dataset.md) for relationship schema definitions.

## Insert

Inserts a successor in a relationship. The values specified map to existing
primary key segments of the target dataset, in the order the segments have been declared.

For instance with a target dataset `tgtds` set as follows:
```sql
CREATE DATASET job PRIMARY KEY(title.name, title.level);
INSERT INTO job VALUES '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}';
```

With a relationship defined on dataset `dev` as:
```sql
CREATE DATASET dev RELATIONSHIP tasks(job);
```

You can now add the `job` item as a `tasks` relationship successor to a `dev` dataset item:
```sql
INSERT INTO dev VALUES '{"idtag": "joe", "greeting": "hi!"}';
INSERT INTO dev.tasks VALUES ('rust guru', 5) WHERE idtag = 'joe';
```

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
--
{"greeting":"hi!","idtag":"joe","tasks":"rust guru 5"}
```

The same projection without summary:
```sql
SELECT d FROM dev d;
--
{"greeting":"hi!","idtag":"joe"}
```
