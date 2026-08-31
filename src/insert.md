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

The `INSERT` statement inserts comma-separated values into a dataset. Each value must be a valid JSON object.

Example:
```sql
INSERT INTO job VALUES
   '{"title": {"name": "rust guru", "level": 5}, "vibe": "good"}',
   '{"title": {"name": "go for", "level": 1}, "vibe": "so so"}';
```
