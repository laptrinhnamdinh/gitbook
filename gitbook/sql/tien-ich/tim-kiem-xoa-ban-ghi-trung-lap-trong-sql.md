# Tìm kiếm, xóa bản ghi trùng lặp trong sql

```sql
WITH cte AS (
    SELECT 
        [Column1],[Column2],
        ROW_NUMBER() OVER (
            PARTITION BY 
                [Column1],[Column2]
            ORDER BY 
               [Column1],[Column2]
        ) row_num
     FROM 
         TABLE_NAME
	)
	--SELECT * FROM cte
	--WHERE row_num > 1 ORDER BY [NewsId];
	DELETE FROM cte
	WHERE row_num > 1;
```
