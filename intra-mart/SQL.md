# SQL

2WaySQLをサポートし、パラメータの埋め込みや条件分岐などの機能を利用して動的にクエリを変化させることができる。
SQLファイルはS2JDBCによって処理されるものと思われる。

参照: [Seasar2 - S2JDBC - JdbcManager - SQLファイルによる操作](http://s2container.seasar.org/2.4/ja/s2jdbc_manager_sqlfile.html)


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
        sample_param_name: DbParameter.string("condition_value")
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
            DbParameter.string("condition_value1"),
            DbParameter.string("condition_value2"),
            DbParameter.string("condition_value3"),
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

## 条件分岐

パラメータの値にて条件判断を行い、条件に該当する場合のみSQL文に含めることができる。
条件に該当しない場合は実行するSQL文から除去される。
`IF`と`END`でブロックを構成し、`IF`には条件文を記載する。

```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN_1 = /*sample_param_name_1*/'sample'
/*IF sample_param_name_2 != null*/
AND SAMPLE_COLUMN_2 = /*sample_param_name_2*/
/*END*/
```

```js
let databaseResult = new TenantDatabase()
    .executeByTemplate(SQL_FILE_PATH, {
        sample_param_name_1: DbParameter.string("condition_value_1")
        sample_param_name_2: DbParameter.string("condition_value_2")
    });
```

### `sample_param_name_2`が`null`の場合に実行されるSQL

```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN_1 = 'condition_value_1'
```

### `sample_param_name_2`が`null`でない場合に実行されるSQL

```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN_1 = 'condition_value_1'
AND SAMPLE_COLUMN_2 = 'condition_value_2'
```

## 条件分岐の結果により不正なSQL文となることを防ぐ

`IF`の条件判断に該当しない場合にSQL文を除去した結果、不正なSQL文となる場合がある。
`BEGIN`と`END`でブロックを構成することで内部のすべての`IF`の条件判断に該当しない場合に
`BEGIN`と`END`の区間すべてのSQL文から除去することができる。

### BEGIN/ENDを使用していない場合

```sql
-- sample_param_name_1がnullの場合WHERE句が空となってしまい、エラーとなる。
SELECT * FROM SAMPLE_TABLE
WHERE
/*IF sample_param_name_1 != null*/
AND SAMPLE_COLUMN_1 = /*sample_param_name_1*/
/*END*/
```

### BEGIN/ENDを使用した場合

```sql
-- sample_param_name_1がnullの場合WHERE句全体が除去される。
SELECT * FROM SAMPLE_TABLE
/*BEGIN*/
    WHERE
    /*IF sample_param_name_1 != null*/
    AND SAMPLE_COLUMN_1 = /*sample_param_name_1*/
    /*END*/
/*END*/
```
