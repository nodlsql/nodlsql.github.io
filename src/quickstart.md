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

