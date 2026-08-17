# nodls
/ˈnoːd(ə)lz/

## Introduction

The [nodls](https://github.com/nodlsql/nodls_demo) server combines an extended SQL query API with a [jsonb](https://docs.rs/jsonb/latest/jsonb/) data model that promotes fast iterating development and maintenance of DBMS applications.

You can check out the sql api usability with the [sqlcmd](https://nodls.org/webdemo/)  web demonstrator.

It compares against MySQL Server as follows:

| Area | nodls | MySQL Server (typical MySQL 8.x) |
|---|---|---|
| Core data model | JSON object collections in datasets | Relational tables (rows/columns), plus JSON column type |
| Main container | `DATASET` | `DATABASE` / `TABLE` |
| Schema style | Flexible JSON shape per item; optional keys | Fixed table schema (typed columns), unless storing semi-structured JSON in JSON columns |
| Transaction model | ACID transactions supported | ACID with InnoDB (default engine) |
| Primary keys | Declared at dataset level, supports multi-segment keys over paths (for example a.b, c) | Declared on table columns; composite keys supported |
| Secondary indexes | Unique and non-unique indexes, including multi-segment/path traversal | B-tree and other index types depending on engine; composite and unique indexes supported |
| Query language | SQL-like with JSON path-oriented expressions | ANSI-style SQL dialect with MySQL extensions |
| JSON querying | Native path expressions and jsonpath directly in predicates/projections | JSON functions/operators (for example JSON_EXTRACT), generated columns often used for indexed JSON access |
| Joins | Supported via multi-dataset FROM and predicates | Full join support (INNER/LEFT/RIGHT/CROSS, etc.) |
| Relationship model | Explicit dataset relationships and navigation (direct + inverse), designed as join alternative | Foreign keys enforce integrity; joins used for navigation |
| Relationship operations | Insert/delete relationship successors with dedicated syntax (for example source.relationship) | No equivalent relationship object syntax; insert/update foreign key column values instead |
| Projection behavior | Supports selecting full object, fields, expressions, relationship-aware projections | Standard SQL projection of columns/expressions; JSON projection via functions |
| Update semantics | Can set nested JSON paths and delete JSON elements in-place | UPDATE sets column values; JSON updates via JSON_SET/JSON_REMOVE-style functions |
| Delete semantics | DELETE dataset items by predicate; relationship successor delete syntax available | DELETE rows by predicate; no native relationship-delete syntax |
| Null/exists checks | Distinguishes field existence (`IS NULL`) from JSON value null comparisons | SQL NULL semantics; JSON null vs SQL NULL can differ and requires function/operator care |
| Data types | JSON primitives/structures: string, number, boolean, null, object, array | Rich SQL scalar types (INT, VARCHAR, DATETIME, etc.) plus JSON |
| Best fit | JSON-first app development with SQL querying and relationship navigation | General-purpose relational workloads, mature ecosystem, broad tooling/compatibility |