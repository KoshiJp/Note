# intra-mart/SQL

SQLファイルはS2JDBCによって処理されるものと思われる。
2WaySQLをサポートし、パラメータの埋め込みや条件分岐などの機能を利用して動的にクエリを変化させることができる。

<small>参照 - [Seasar2 - S2JDBC - JdbcManager - SQLファイルによる操作](http://s2container.seasar.org/2.4/ja/s2jdbc_manager_sqlfile.html)</small>


##### パラメータの置き換え
下記SQLをツールで実行する場合は`'sample'`という値での選択条件となる。
intra-martで実行する際にはスクリプトから渡すパラメータの値にて置き換えて実行される。下記のスクリプトの例ではSQLの選択条件値`'sample'をパラメータ`sample_param_name`の値`'condition_value'`に置き換えて実行される。
```sql
SELECT * FROM SAMPLE_TABLE
WHERE SAMPLE_COLUMN = /*sample_param_name*/'sample'
```
```js
let databaseResult = new TenantDatabase()
    .executeByTemplate(SQL_FILE_PATH, {
        sample_param_name: 'condition_value'
    });
```