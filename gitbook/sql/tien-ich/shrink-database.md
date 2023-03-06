---
description: Code shrink database in SQL
---

# Shrink Database

```sql
ALTER DATABASE DBName SET RECOVERY SIMPLE;
DBCC SHRINKFILE (DBName_log, 1);
ALTER DATABASE DBName  SET RECOVERY FULL;
```
