# Insert

Inserts comma separated values into a dataset. The values should contain valid json objects.

```sql
INSERT INTO job VALUES
   '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}',
   '{"title": {"name": "go for", "level": 1}, "vibe": "so so"}';
```