# Hàm tính tuổi theo ngày tháng năm sinh | Caculate old by dateofbirth

```sql
ALTER Function [dbo].[fnTinhTuoiTheoThang] (
@FromDate DATETIME,
@ToDate DATETIME
)RETURNS INTEGER
BEGIN
  SET @FromDate=DATEADD(month, DATEDIFF(month, 0, @FromDate), 0)
  SET @ToDate=DATEADD(month, DATEDIFF(month, 0, @ToDate), 0)
  RETURN CONVERT(int,ROUND(DATEDIFF(hour,@FromDate,@ToDate)/8766.0,0))
END
```

