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

# JSONPath

JSONPath expressions can be combined with alias or relationship navigation.

See the [Databend Labs JSONB](https://github.com/databendlabs/jsonb) project for supported JSONPath syntax.

For example, to find the employee of the year:
```sql
INSERT INTO dev VALUES
  '{"idtag": "joe", "greeting": "hi!", "kudos": [{"eoy":2020}, {"eoy":2026}]}';
SELECT idtag, kudos[0] FROM dev WHERE kudos[0] IS NOT NULL;
SELECT idtag, kudos[*]?(@.eoy >= 2020) FROM dev WHERE kudos IS NOT NULL;
```

JSONPath preceded with alias `d` and relationship `tasks`:
```sql
SELECT d.tasks.$.* FROM dev d;
```

The `*` path element behaves differently depending on context. At the top level, it returns the full JSON object content.
```sql
SELECT * FROM dev WHERE idtag = 'joe';
```
Select result:
```
{"greeting":"hi!","idtag":"joe","kudos":[{"eoy":2020},{"eoy":2026}]}
```

If `*` is used within a JSONPath expression, it flattens the JSON object. For instance from the `$` root element:
```sql
SELECT $.* FROM dev WHERE idtag = 'joe';
```
Select result:
```
["hi!","joe",[{"eoy":2020},{"eoy":2026}]]
```
