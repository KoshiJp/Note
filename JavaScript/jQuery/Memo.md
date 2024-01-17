# メモ

## map

第一引数がインデックス、第二引数が要素。

```js
let result = $(SELECTOR).map(function(index, element) { /*...*/ });
```

## filter

第一引数がインデックス、第二引数が要素。

```js
let result = $(SELECTOR).map(function(index, element) { /*...*/ });
```

## each

第一引数がインデックス、第二引数が要素。

```js
$(SELECTOR).map(function(index, element) { /*...*/ });
```

## toArray

jQueryオブジェクトをJavascriptの配列に変換する。

```js
let result = $(SELECTOR).toArray();
```

## ラジオボタンの選択状態を取得する

`prop`関数に`"checked"`を渡すとラジオボタンの選択状態を取得できる。

```js
let value = $("input[name=RADIO_BUTTON_NAME]").prop("checked");
```

## 選択されているラジオボタンの値を取得する

`:checked`疑似要素で要素を絞り込み、`val`関数で値を取得することで選択されたラジオボタンの値を取得できる。

```js
let value = $("input[name=RADIO_BUTTON_NAME]").filter(":checked").val();
```

## チェックボックスのチェック状態を取得する

`prop`関数に`"checked"`を渡すとチェックボックスのチェック状態を取得できる。

```js
let value = $("input[name=CHECK_BOX_NAME]").prop("checked");
```

## セレクトボックスの選択されている値を取得する

子の`option`要素の`:selected`疑似要素で要素を絞り込み、`val`関数で値を取得することで選択された値を取得できる。

```js
let value = $("select[name=SELECT_BOX_NAME]").children(":selected").val();
```

## セレクトボックスの選択状態を設定する

子の`option`要素を絞り込み、`selected`属性を設定することで選択を設定できる。

```js
let value = $("select[name=SELECT_BOX_NAME]").children("[value='VALUE']").prop("selected", true);
```
