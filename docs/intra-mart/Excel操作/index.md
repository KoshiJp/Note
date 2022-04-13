# intra-mart/Excel操作

Apache POIを使用してExcelワークブックを操作できる。

##### 手順
1. `java.io.FileInputStream`を使用して編集対象ファイルを開く。
1. `org.apache.poi_v3_8.ss.usermodel.WorkbookFactory`オブジェクトを生成する。
1. `WorkbookFactory#create`で`Workbook`オブジェクトを作成する。
1. `Workbook`オブジェクトを通じてワークブックを編集する。
1. `java.io.FileOutputStream`を使用して保存先ファイルを開く。
1. `Workbook#write`で編集結果をファイルに出力する。

##### `java.io.FileInputStream`を使用して編集対象ファイルを開く。
```js
let inputStream = new java.io.FileInputStream(path);
```
##### `org.apache.poi_v3_8.ss.usermodel.WorkbookFactory`オブジェクトを生成する。
```js
let workbookFactory = new Packages.org.apache.poi_v3_8.ss.usermodel.WorkbookFactory();
```

##### `WorkbookFactory#create`で`Workbook`オブジェクトを作成する。
```js
workbookFactory.create(inputStream);
```

##### `java.io.FileOutputStream`を使用して保存先ファイルを開く。
```js
let outputStream = new java.io.FileOutputStream(path);
```

##### `Workbook#write`で編集結果をファイルに出力する。
```js
workbook.write(outputStream);
```
