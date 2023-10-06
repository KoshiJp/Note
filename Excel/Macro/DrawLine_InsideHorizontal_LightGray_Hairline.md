# 選択セル範囲に罫線を引く

```vba
'==================================================
'選択セル範囲に罫線を引く
'箇所   : xlInsideVertical 内側垂直線
'線種   : xlContinuous 実線
'色     : 1 テーマカラー1(標準では薄いグレー)
'明るさ : -0.25
'         (最も暗い(-1)～最も明るい(1))
'太さ   : xlHairline 細線(最も細い罫線)
'==================================================
Public Sub DrawLine_InsideVertical_LightGray_Hairline()
    With Selection.Borders(xlInsideVertical)
        .LineStyle = xlContinuous
        .ThemeColor = 1
        .TintAndShade = -0.25
        .Weight = xlHairline
    End With
End Sub
```
