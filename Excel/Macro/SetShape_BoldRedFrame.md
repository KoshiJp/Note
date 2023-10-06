# 選択中のShapeを赤枠にする

```vba
'==================================================
'選択中のShapeを赤枠にする。
'==================================================
Sub SetShape_BoldRedFrame()
    Dim sr As ShapeRange
    Set sr = Selection.ShapeRange

    sr.Fill.Visible = msoFalse
    With sr.Line
        .Visible = msoTrue
        .ForeColor.RGB = RGB(255, 0, 0)
        .Transparency = 0
    End With
    With sr.Line
        .Visible = msoTrue
        .Weight = 2.25
    End With
End Sub
```
