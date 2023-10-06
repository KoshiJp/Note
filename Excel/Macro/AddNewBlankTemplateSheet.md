# 新しい白紙シートを生成する

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
