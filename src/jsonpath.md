# Jsonpath

Jsonpath expressions can be combined with alias or relationship navigation.

See also [Databend Labs jsonb](https://github.com/databendlabs/jsonb) for supported jsonpath syntax.

For example to select who has been employee of the year:
```sql
INSERT INTO dev VALUES '{"idtag": "joe", "greeting": "hi!", "kudos": [{"eoy":2020}, {"eoy":2026}]}';
SELECT idtag, kudos[0] FROM dev WHERE kudos[0] IS NOT NULL;
SELECT idtag, kudos[*]?(@.eoy >= 2020) FROM dev WHERE kudos IS NOT NULL;
```

Jsonpath preceded with alias `d` and relationship `tasks`:
```sql
SELECT d.tasks.$.* FROM dev d;
```

The `*` path element behavior is context dependent. If used at top level it selects all, and includes a relationship summary in the result:
```sql
SELECT * FROM dev WHERE idtag = 'joe';
```
Select result:
```sql
{"greeting":"hi!","idtag":"joe","kudos":[{"eoy":2020},{"eoy":2026}]}
```

If `*` is used from within a jsonpath it flattens the json object. For instance from the `$` root element:
```sql
SELECT $.* FROM dev WHERE idtag = 'joe';
```
Select result:
```sql
["hi!","joe",[{"eoy":2020},{"eoy":2026}]]
```
