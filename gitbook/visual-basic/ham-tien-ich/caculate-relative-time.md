---
description: Caculate Relative time
---

# Caculate Relative time

```vbnet
 Public Shared Function RelativeTime(ByVal myDate As DateTime) As String
        If myDate.Year < 1900 Then
            RelativeTime = ""
            Exit Function
        End If
        Const SECOND As Integer = 1
        Const MINUTE As Integer = 60 * SECOND
        Const HOUR As Integer = 60 * MINUTE
        Const DAY As Integer = 24 * HOUR
        Const MONTH As Integer = 30 * DAY
        Dim ts = New TimeSpan(DateTime.Now.Ticks - myDate.Ticks)
        Dim delta As Double = Math.Abs(ts.TotalSeconds)
        If delta < 1 * MINUTE Then Return If(ts.Seconds = 1, "1 giây trước", ts.Seconds & " giây trước")
        If delta < 2 * MINUTE Then Return "1 phút trước"
        If delta < 45 * MINUTE Then Return ts.Minutes & " phút trước"
        If delta < 90 * MINUTE Then Return "1 giờ trước"
        If delta < 24 * HOUR Then Return ts.Hours & " giờ trước"
        If delta < 48 * HOUR Then Return "1 ngày trước"
        If delta < 30 * DAY Then Return ts.Days & " ngày trước"
        If delta < 12 * MONTH Then
            Dim months As Integer = Convert.ToInt32(Math.Floor(CDbl(ts.Days) / 30))
            Return If(months <= 1, "1 tháng trước", months & " tháng trước")
        Else
            Dim years As Integer = Convert.ToInt32(Math.Floor(CDbl(ts.Days) / 365))
            Return If(years <= 1, "1 năm trước", years & " năm trước")
        End If
    End Functionsq
```
