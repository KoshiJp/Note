# 選択中のセルを赤枠にする

```vba
'==================================================
'選択中のセルを赤枠にする。
'==================================================
Sub SetRange_BoldRedFrame()
    With Selection.Borders(xlEdgeLeft)
        .LineStyle = xlContinuous
        .Color = -16776961
        .TintAndShade = 0
        .Weight = xlMedium
    End With
    With Selection.Borders(xlEdgeTop)
        .LineStyle = xlContinuous
        .Color = -16776961
        .TintAndShade = 0
        .Weight = xlMedium
    End With
    With Selection.Borders(xlEdgeBottom)
        .LineStyle = xlContinuous
        .Color = -16776961
        .TintAndShade = 0
        .Weight = xlMedium
    End With
    With Selection.Borders(xlEdgeRight)
        .LineStyle = xlContinuous
        .Color = -16776961
        .TintAndShade = 0
        .Weight = xlMedium
    End With
End Sub
```
