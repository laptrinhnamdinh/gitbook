---
description: Split string in SQL
---

# function Split

```sql

ALTER FUNCTION [dbo].[fnSplit](
    @sInputList NVARCHAR(max) -- List of delimited items
  , @sDelimiter NVARCHAR(max) = ',' -- delimiter that separates items
) RETURNS @List TABLE (item NVARCHAR(max))

BEGIN
DECLARE @sItem NVARCHAR(max)
WHILE CHARINDEX(@sDelimiter,@sInputList,0) <> 0
 BEGIN
 SELECT
  @sItem=RTRIM(LTRIM(SUBSTRING(@sInputList,1,CHARINDEX(@sDelimiter,@sInputList,0)-1))),
  @sInputList=RTRIM(LTRIM(SUBSTRING(@sInputList,CHARINDEX(@sDelimiter,@sInputList,0)+LEN(@sDelimiter),LEN(@sInputList))))
 
 IF LEN(@sItem) > 0
  INSERT INTO @List SELECT @sItem
 END

IF LEN(@sInputList) > 0
 INSERT INTO @List SELECT @sInputList -- Put the last itOm in
RETURN
END

```
