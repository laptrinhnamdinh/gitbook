---
description: Đếm các bản ghi của toàn bộ các bảng trong SQL
---

# Đếm các bản ghi của toàn bộ các bảng trong SQL

```sql
SELECT  (SCHEMA_NAME(A.schema_id) + '.' + A.Name) AS TableName  
, SUM(B.rows) AS RecordCount  
FROM sys.objects A  
INNER JOIN sys.partitions B ON A.object_id = B.object_id  
WHERE A.type = 'U'  
GROUP BY A.schema_id, A.Name  
ORDER BY RecordCount desc
```
