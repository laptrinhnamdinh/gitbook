---
description: Hàm tính vote 5 sao trong SQL - Caculate percent of vote In SQL
---

# Hàm tính vote 5 sao - Caculate percent of vote

```sql
DECLARE @Star1 AS INTEGER, @Star2 AS INTEGER, @Star3 AS INTEGER, @Star4 AS INTEGER, @Star5 AS INTEGER
DECLARE @Svote AS FLOAT = 0	
SET @Star1=(SELECT COUNT(1) FROM dbo.CMS_ReviewM WHERE Stars=1 )
SET @Star2=(SELECT COUNT(1) FROM dbo.CMS_ReviewM WHERE Stars=2 )
SET @Star3=(SELECT COUNT(1) FROM dbo.CMS_ReviewM WHERE Stars=3 )
SET @Star4=(SELECT COUNT(1) FROM dbo.CMS_ReviewM WHERE Stars=4 )
SET @Star5=(SELECT COUNT(1) FROM dbo.CMS_ReviewM WHERE Stars=5 )
	
DECLARE @TS FLOAT = 5 * @Star5 + 4 * @Star4 + 3 * @Star3 + 2 * @Star2 + 1 * @Star1
DECLARE @MS FLOAT	= @Star1 + @Star2 + @Star3 + @Star4 + @Star5
IF @MS>0
BEGIN
	SET @Svote=@TS/@MS
END
	RETURN @Svote
```
