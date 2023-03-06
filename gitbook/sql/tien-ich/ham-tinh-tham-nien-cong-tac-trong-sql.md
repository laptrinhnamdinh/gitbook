---
description: Hàm tính thâm niên công tác cho SQL
---

# Hàm tính thâm niên công tác trong SQL

```sql
SELECT CAST(DATEDIFF(yy, @NgayBatDau, @NgayKetThuc) AS varchar(4)) +' năm '+
       CAST(DATEDIFF(mm, DATEADD(yy, DATEDIFF(yy, @NgayBatDau, @NgayKetThuc), @NgayBatDau), @NgayKetThuc) AS varchar(2)) +' tháng '+
       CAST(DATEDIFF(dd, DATEADD(mm, DATEDIFF(mm, DATEADD(yy, DATEDIFF(yy, @NgayBatDau, @NgayKetThuc), @NgayBatDau), @NgayKetThuc), DATEADD(yy, DATEDIFF(yy, @NgayBatDau, @NgayKetThuc), @NgayBatDau)), @NgayKetThuc) AS varchar(2)) +' ngày' 
```
