# intra-mart/SQL

SQLファイルはS2JDBCによって処理されるものと思われる。
2WaySQLをサポートし、パラメータの埋め込みや条件分岐などの機能を利用して動的にクエリを変化させることができる。

<small>参照 - [Seasar2 - S2JDBC - JdbcManager - SQLファイルによる操作](http://s2container.seasar.org/2.4/ja/s2jdbc_manager_sqlfile.html)</small>


## リテラル値の置換
リテラル値をパラメータの値で置き換えることができる。
リテラル値の左にSQLコメントを`/*PARAM_NAME*/`のように記載する。

下記SQLとスクリプトの例では、
SQLをツールで実行する場合は`'sample'`というリテラル値での選択条件となる。
intra-martで実行する際にはリテラル値`'sample'`をパラメータ`sample_param_name`の値`'condition_value'`に置き換えて実行される。

```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN = /*sample_param_name*/'sample'
```
```js
let databaseResult = new TenantDatabase()
    .executeByTemplate(SQL_FILE_PATH, {
        sample_param_name: DbParameter.string('condition_value')
    });
```

## IN句の置換
IN句の複数のリテラル値をパラメータの配列の値で置き換えることができる。
SQLのリテラル値の数とパラメータの配列の要素数は一致させる必要がある。

```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN IN /*sample_params*/('value1', 'value2', 'value3')
```
```js
let databaseResult = new TenantDatabase()
    .executeByTemplate(SQL_FILE_PATH, {
        sample_params: [
            DbParameter.string('condition_value1'),
            DbParameter.string('condition_value2'),
            DbParameter.string('condition_value3'),
        ]
    });
```

## SQLの埋め込み
パラメータの文字列をSQL文に埋め込むことができる。
埋め込み箇所にパラメータ名の先頭に`'$'`を付与したSQLコメントを`/*$PARAM_NAME*/`のように記載する。

パラメータはDbParameterオブジェクトではなく文字列を指定すればよい。

```sql
SELECT /*$top*/ * FROM SAMPLE_TABLE
```
```js
let databaseResult = new TenantDatabase()
    .executeByTemplate(SQL_FILE_PATH, {
        top: "TOP(100)"
    });
```

