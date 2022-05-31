# Excel / マクロ

# 新しい白紙シートを生成する

###### Excel-VBA
```vba
'==================================================
'新しい白紙シートを生成する
'==================================================
Public Sub AddNewBlankTemplateSheet()
    On Error GoTo OnError
    Application.ScreenUpdating = False
    
    ' 新しいシートのシート名を生成する。
    Dim NewSheetBaseName As String
    NewSheetBaseName = "白紙"
    Dim NewSheetNameSuffixNumber As Integer
    NewSheetNameSuffixNumber = 0
    Dim NewSheetNameSuffix As String
    NewSheetNameSuffix = ""
    Dim NewSheetName As String
    Do
        NewSheetName = NewSheetBaseName & NewSheetNameSuffix
        Dim SheetFound As Boolean
        SheetFound = False
        Dim s As Variant
        For Each s In Sheets
            If s.Name = NewSheetName Then
                SheetFound = True
                Exit For
            End If
        Next
        If SheetFound = False Then
            Exit Do
        End If
        NewSheetNameSuffixNumber = NewSheetNameSuffixNumber + 1
        NewSheetNameSuffix = CStr(NewSheetNameSuffixNumber)
    Loop
    
    ' 新しいシートを生成する。
    Dim NewSheet As Worksheet
    Set NewSheet = Sheets.Add(After:=ActiveSheet)
    NewSheet.Name = NewSheetName

    ' 新しいシートの内容を設定する。
    NewSheet.Cells.Font.Name = "メイリオ"
    NewSheet.Cells.Font.Size = 8
    NewSheet.Cells.HorizontalAlignment = xlGeneral
    NewSheet.Cells.VerticalAlignment = xlTop
    NewSheet.Cells.NumberFormatLocal = "@"
    NewSheet.Cells.ColumnWidth = 3
    
    ' カーソル位置をA1に設定する。
    NewSheet.Range("A1").Select

Exit Sub
OnError:
    Application.ScreenUpdating = True
End Sub
```

# 選択セル範囲に罫線を引く

###### Excel-VBA
```vba
'==================================================
'選択セル範囲に罫線を引く
'箇所   : xlInsideHorizontal 内側水平線
'線種   : xlContinuous 実線
'色     : 1 テーマカラー1(標準では薄いグレー)
'明るさ : -0.25
'         (最も暗い(-1)～最も明るい(1))
'太さ   : xlHairline 細線(最も細い罫線)
'==================================================
Public Sub DrawLine_InsideHorizontal_LightGray_Hairline()
    With Selection.Borders(xlInsideHorizontal)
        .LineStyle = xlContinuous
        .ThemeColor = 1
        .TintAndShade = -0.25
        .Weight = xlHairline
    End With
End Sub
```

# 選択セル範囲に罫線を引く

###### Excel-VBA
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

# 選択中のセルを赤枠にする

###### Excel-VBA
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

# 選択中のShapeを赤枠にする

###### Excel-VBA
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