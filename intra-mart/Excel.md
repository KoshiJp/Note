# intra-mart / Excel

Apache POIを使用してExcelワークブックを操作できる。

参照: [Overview (POI API Documentation)](https://poi.apache.org/apidocs/dev/overview-summary.html)

## Excelワークブックの基本的な操作手順

1. `java.io.FileInputStream`を使用して編集対象ファイルを開く。
1. `org.apache.poi_v3_8.ss.usermodel.WorkbookFactory`オブジェクトを生成する。
1. `WorkbookFactory#create`で`Workbook`オブジェクトを作成する。
1. `Workbook`オブジェクトを通じてワークブックを編集する。
1. `java.io.FileOutputStream`を使用して保存先ファイルを開く。
1. `Workbook#write`で編集結果をファイルに出力する。

### `java.io.FileInputStream`を使用して編集対象ファイルを開く

```js
let inputStream = new java.io.FileInputStream(path);
```

### `org.apache.poi_v3_8.ss.usermodel.WorkbookFactory`オブジェクトを生成する

```js
let workbookFactory = new Packages.org.apache.poi_v3_8.ss.usermodel.WorkbookFactory();
```

### `WorkbookFactory#create`で`Workbook`オブジェクトを作成する

```js
workbookFactory.create(inputStream);
```

### `java.io.FileOutputStream`を使用して保存先ファイルを開く

```js
let outputStream = new java.io.FileOutputStream(path);
```

### `Workbook#write`で編集結果をファイルに出力する

```js
workbook.write(outputStream);
```

## Excelワークブック編集API

Excelワークブックの内容は、操作対象に対応するクラスのインスタンスを通じて操作する。

ワークブックは`Workbook`オブジェクトを通じて行う。
ワークシートは`Worksheet`オブジェクト、行は`Row`オブジェクト、セルは`Cell`オブジェクトを通じて行う。

### ワークシートを取得する

```js
// インデックスを指定してワークシートを取得する。
workbook.getSheetAt(index);
```

### 行を取得する

```js
// インデックスを指定して行を取得する。
// 行が存在しない場合、nullが返却される。
let row = worksheet.getRow(rowIndex);
```

### 行を作成する

```js
// インデックスを指定して行を作成する。
let neRow = worksheet.createRow(rowIndex);
```

### セルを取得する

```js
// インデックスを指定してセルを取得する。
// セルが存在しない場合、nullが返却される。
let cell = row.getCell(columnIndex);
```

### セルを作成する

```js
// インデックスを指定してセルを作成する。
let newCell = row.createCell(columnIndex);
```

### セルの値を設定する

```js
cell.setCellValue(value);
```
