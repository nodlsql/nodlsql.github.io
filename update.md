# Update

Update or delete json elements in existing dataset items.

```sql
UPDATE job SET title.level = 2, vibe = 'better' WHERE vibe <> 'good';
UPDATE job DELETE vibe, title.level WHERE vibe = 'bad';
```