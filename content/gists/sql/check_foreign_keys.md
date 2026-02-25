---
title: "check foreign keys in mySQL"
date: "2023-11-26T16:30:00+01:00"
tags: ["sql", "foreign keys", "gist"]
---

```SQL
SELECT refcons.TABLE_NAME,
       refcons.REFERENCED_TABLE_NAME,
       refcons.CONSTRAINT_NAME,
       keycol.COLUMN_NAME
FROM information_schema.REFERENTIAL_CONSTRAINTS refcons
         JOIN information_schema.KEY_COLUMN_USAGE keycol ON (
            refcons.CONSTRAINT_SCHEMA = keycol.TABLE_SCHEMA AND
            refcons.TABLE_NAME = keycol.TABLE_NAME AND
            refcons.CONSTRAINT_NAME = keycol.CONSTRAINT_NAME)
WHERE refcons.CONSTRAINT_SCHEMA = 'db_name'
  AND (refcons.TABLE_NAME = 'table' OR refcons.REFERENCED_TABLE_NAME = 'table');
```

https://gist.github.com/pashamray/eac6a730b4033f315a5cf9e2c50ca112
