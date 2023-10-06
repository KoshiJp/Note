# PowerShell

## 文字

### 改行

特殊文字はバッククオート``` ` ```でエスケープする。

```powershell
"`r`n"
```

## 引数

### 残余引数

```powershell
Param([Parameter(ValueFromRemainingArguments)]$Remaining)
```

## カスタムオブジェクト

```powershell
[PSCustomObject]@{
    Name1       = $Value1;
    Name2       = $Value2;
}
```

## 関数

```powershell
Function Show-Sample() {
    [CmdletBinding()]
    [CmdletBinding(DefaultParameterSetName = "Param")]
    param(
        [Parameter(Mandatory, ValueFromPipeline, ParameterSetName = "Pipeline")]
        [Parameter(Mandatory, Position = 0, ParameterSetName = "Param")]
        [string[]]$Arg1,
        [Parameter(Mandatory, Position = 0, ParameterSetName = "Pipeline")]
        [Parameter(Mandatory, Position = 1, ParameterSetName = "Param")]
        [string]$Arg2
    )
    begin {
        # ...
    }
    process {
        $Arg1 | Format-Table | Out-Default
        $Arg2 | Format-Table | Out-Default
    }
    end {
        # ...
    }
}
```

## クラス

```powershell
Class Sample {
    # プロパティ
    $Variable

    # 静的メソッド
    static [void] SampleStaticMethod($Arg1, $Arg2) {
        # ...
    }

    # コンストラクタ
    Sample(){
        # ...
    }

    # メソッド
    [void] SampleInstanceMethod($Arg1, $Arg2) {
        # ...
    }
}
```

## デバッグメッセージ

### 出力設定

```powershell
# デバッグメッセージを表示して続行する。
$DebugPreference = 'Continue'
# デバッグメッセージを表示しないで続行する。
$DebugPreference = 'SilentlyContinue' 
```

### 出力

```powershell
Write-Debug
```

## エラー

### エラー取得

```powershell
Get-Error
```

## 非停止エラーの対応

```powershell
# PowerShellの終了しないエラーが発生した場合にスクリプト実行を停止するため、自動変数'$ErrorActionPreference'に'Stop'を設定する。
$ErrorActionPreference = 'Stop'
```
