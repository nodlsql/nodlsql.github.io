# Quick start

At the [sqlcmd](https://nodls.org/webdemo/) prompt, run the following commands to create and query your first dataset:

```sql
CREATE DATASET job;
INSERT INTO job VALUES '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}';
SELECT * from job WHERE vibe = 'good';
```
Select result:
```sql
{"title":{"level":5,"name":"rust guru"},"vibe":"good"}
```

