# SQL Server/メモ

## NULL値を指定の値に置き換える

`ISNULL(check_expression, replacement_value)`

##### check_expression
NULL かどうかを調べる式
##### replacement_value
check_expression が NULL の場合に返される式

参照: [ISNULL (Transact-SQL) - docs.microsoft.co](https://docs.microsoft.com/ja-jp/sql/t-sql/functions/isnull-transact-sql)

## 指定された2つの式が等しい場合にNULL値を返す

`NULLIF(expression, expression)`

##### expression
任意の有効なスカラー式です。

参照: [NULLIF (Transact-SQL) - docs.microsoft.co](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/nullif-transact-sql)