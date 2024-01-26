# すべてのワークシートでA1セルを選択した状態にする

```vba
'==================================================
'すべてのワークシートでA1セルを選択した状態にする
'==================================================
Public Sub SelectRangeA1ForAllWorksheet()
    On Error Resume Next
    Application.ScreenUpdating = False
    Dim CurrentWorksheet As Variant
    For Each CurrentWorksheet In ActiveWorkbook.Worksheets
        Call CurrentWorksheet.Select
        Call CurrentWorksheet.Range("A1").Select
        ActiveWindow.ScrollRow = 1
        ActiveWindow.ScrollColumn = 1
    Next
    Application.ScreenUpdating = True
    Call ActiveWorkbook.Sheets(1).Select
End Sub
```
