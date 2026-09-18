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

# Insert

The `INSERT` statement inserts comma-separated data items and associated relationship elements into a dataset. Each data item value must be a valid JSON object.

Example:
```sql
CREATE DATASET job
    PRIMARY KEY(title.name, title.level);
INSERT INTO job VALUES
   '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}',
   '{"title": {"name": "sql defender", "level": 4}, "vibe": "okay"}',
   '{"title": {"name": "go for", "level": 1}, "vibe": "so so"}';
```

To insert relationship elements into the `tasks` and `errands` relationships for `joe` and `mary`:
```sql
CREATE DATASET dev
    RELATIONSHIP tasks(job)
    RELATIONSHIP errands(job);
INSERT INTO dev VALUES
    '{"idtag": "joe", "greeting": "hi!"}' tasks ('rust guru', 5) ('sql defender', 4) errands ('go for', 1),
    '{"idtag": "mary", "greeting": "hello!"}' tasks ('rust guru', 5);
```

The specified relationship values map to the target dataset's existing primary key segments, in the order they are declared.