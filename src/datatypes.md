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

# Data types

The standard JSON data types are supported:
| Data type | Description | Example |
| -------- | ----------- | ------- |
| String | Text enclosed in double quotes | "hello" |
| Number | Integer or floating-point number | 42, 3.14 |
| Boolean | True or false values | true, false |
| Null | An empty value | null |
| Object | Unordered key-value pairs | {"id": 1} |
| Array | Ordered list of values | [1, 2, 3]

String constants are enclosed in single quotes when expressed in the query syntax:
```sql
SELECT * FROM dev WHERE idtag = 'joe';
```

In the result set string scalar values and json objects are returned with no embedding quotes:
```sql
SELECT vibe, title.level, title FROM job WHERE vibe <> 'so so';
```
Select result:
```sql
good, 5, {"level":5,"name":"rust guru"}
```

