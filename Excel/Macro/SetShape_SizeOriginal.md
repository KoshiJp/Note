# アクティブシート内のすべてのオブジェクトのサイズを100%にする

```vba
'==================================================
'アクティブシート内のすべてのオブジェクトのサイズを100%にする。
'==================================================
Sub SetShape_SizeOriginal()
    Dim v As Variant
    Dim s As Shape
    For Each v In ActiveSheet.Shapes
        Set s = v
        Debug.Print s.Name & " : " & s.Width & "," & s.Height
        s.ScaleHeight 1, msoFalse, msoScaleFromTopLeft
        Debug.Print " => " & s.Width & "," & s.Height
    Next
    
End Sub
```
