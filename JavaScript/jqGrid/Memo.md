# jqGrid

[jqGrid wiki](http://www.trirand.com/jqgridwiki/doku.php)

## ソート順を取得する

```js
let sortIndex1 = $('#sample-list').jqGrid("getGridParam", "sortname");

let sortIndex2 = $('#sample-list').getGridParam("sortname");
```

## ソート方向を取得する

```js
let sortOrde1 = $('#sample-list').jqGrid("getGridParam", "sortorder");

let sortOrde2 = $('#sample-list').getGridParam("sortorder");
```

## 表の再読込を行う

```js
$('#sample-list').trigger('reloadGrid');
```

## 選択されている行のIDの配列を取得する

```js
$('#sample-list').getGridParam('selarrrow');
```

## すべての行のデータを取得する

```js
let rowDataArray1 = $('#sample-list').jqGrid("getRowData");

let rowDataArray2 = $('#sample-list').getRowData();
```

## 指定の行のデータを取得する

```js
let rowData1 = $('#sample-list').jqGrid("getRowData", id);

let rowData2 = $('#sample-list').getRowData(id);
```
