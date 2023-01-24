---
layout: default
title: PostGress SQL indexing
parent: Database
nav_order: 1
permalink: /db-1-PostGress SQL indexing quick notes/
---
# PostGress SQL indexing quick notes

- List all the indexes created on the table 
```roomsql
SELECT * FROM pg_indexes WHERE tablename = 'table-name';
```
- Analysis SQL query
```roomsql
EXPLAIN ANALYZE  SELECT col1 FROM table_name WHERE col2 = 'value' ORDER BY col2 DESC LIMIT 1
```