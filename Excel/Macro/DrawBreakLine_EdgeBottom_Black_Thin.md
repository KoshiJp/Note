# グループの区切りに罫線を引く

```vba
'==================================================
'グループの区切りに罫線を引く
'==================================================
Public Sub DrawBreakLine_EdgeBottom_Black_Thin()
    If Selection.Areas.Count > 1 Then
        MsgBox "このマクロは複数の選択範囲に対しては機能しません。", vbOKCancel, "DrawBreakLine_EdgeBottom_Black_Thin"
        Exit Sub
    End If
    Dim RowEnd As Integer
    RowEnd = Selection.Row + Selection.Rows.Count - 1
    Dim ColumnStart As Integer
    ColumnStart = Selection.Column
    Dim ColumnEnd As Integer
    ColumnEnd = Selection.Column + Selection.Columns.Count - 1
    Dim Cursor As Range
    Set Cursor = ActiveCell
    Do While Cursor.Row <= RowEnd
        If Cursor.Value2 <> Cursor.Offset(1, 0).Value2 Then
            Dim RangeStart As Range
            Set RangeStart = Cursor.Worksheet.Cells(Cursor.Row, ColumnStart)
            Dim RangeEnd As Range
            Set RangeEnd = Cursor.Worksheet.Cells(Cursor.Row, ColumnEnd)
            Dim DrawTargetRange As Range
            Set DrawTargetRange = Cursor.Worksheet.Range(RangeStart, RangeEnd)
            With DrawTargetRange.Borders(xlEdgeBottom)
                .LineStyle = xlContinuous
                .ColorIndex = 0
                .TintAndShade = 0
                .Weight = xlThin
            End With
        End If
        Set Cursor = Cursor.Offset(1, 0)
    Loop
End Sub
```
