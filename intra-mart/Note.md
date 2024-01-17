# / Note

## ページ

### ページテンプレート

ページテンプレートは`.html`ファイルと同名`.js`ファイルのペアで構成される。`.js`ファイルは「ファンクションコンテナ」と呼称される。
`WEB-INF/jssp/src`の配下に配置することでintra-martによって処理され動的にページが生成されるようになる。

### ファンクションコンテナ

ページテンプレートを構成するファイルの内の`.js`ファイル。
ファンクションコンテナの`init`関数はページ初期化処理としてintra-martから呼び出される。
ファンクションコンテナの最上位スコープで宣言した変数は`.html`ファイルにて利用でき、ページへの値の埋め込みに利用できる。

### テンプレートファイル

ページテンプレートを構成するファイルの内の`.html`ファイル。
`.html`ファイルでは通常のHTMLにてページテンプレートを記述する。
`imart`タグを使用することで動的なページ構築を行うことができる。

### imartタグ

`imart`タグは様々な機能を持ち、`type`属性にて機能を指定する。機能により追加のパラメータを属性の形で指定するが、ダブルクォーテーションで括られた値は文字列リテラルと判別される。ファンクションコンテナで宣言した変数を利用する場合は通常のHTMLと異なりダブルクォーテーションで括らないで値を記述する。

### imartタグのメッセージ展開

imartタグに与えるパラメータ属性に`%`で始まる文字列を指定した場合はメッセージIDとして扱われ、intra-martにより対応するロケールのメッセージ文字列へ展開される。

### テンプレートファイルに別のページを埋め込む

`imart`タグの`type`属性に`include`を指定すると別のページを埋め込む機能を利用できる。
`page`属性にスクリプトのパスを指定する。`page`以外の名前の属性とその値は、埋め込みページのファンクションコンテナの`init`関数の最初の引数にオブジェクトのプロパティとして渡されるため、埋め込みページの初期化処理で利用できる。

### デバッグ

`Debug`オブジェクトにデバッグ用関数が定義されているため、活用するとよい。<br/>
`browse`関数では引数に指定した変数の情報をブラウザに表示させることができる。<br/>
`console`関数では引数に指定したオブジェクトをJSON文字列形式にてコンソールへ出力することができる。<br/>
`print`関数ではメッセージをコンソールへ出力することができる。<br/>
`write`関数ではメッセージをファイルへ出力することができる。出力ファイルはホームディレクトリ直下の debug.txt 。ホームディレクトリは標準設定では「WEB-INF」。<br/>

## IM-共通マスタ 検索画面

HTMLのHEADに`imart`タグを記載する。`type`属性は`imACMSearchDialog`とする。これにより共通マスタ検索画面のJavascriptとcssが読み込まれる。
クライアントスクリプトにて`imACMSearchDialog`オブジェクトの`open`関数を呼び出すと、IM-共通マスタ検索画面を呼び出すことができる。

### パラメータ構造

`type`パラメータは`single`か`multiple`のいずれかを指定する。

```js
let parmeter = {
    tabs : [
        {
                id    : 'jp.co.intra_mart.master.app.search.tabs.user.list_user',
                title : 'title'
        }
    ],
    prop : {
        'jp.co.intra_mart.master.app.search.tabs.user.list_user' : [
            'user_cd',
            'user_name'
        ]
    },
    callback_function : '',
    basic_area : '',
    wnd_title : '',
    message : '',
    wnd_close : true,
    type : 'single|multiple',
    deleted_data : false,
    target_locale : '',
    additional_disp : true,
    additional_user_search_name : true,
    additional_dept : true,
    'criteria' : {}
};
```

## サーバーサイドバリデーション

ファンクションコンテナの関数に所定の形式のドキュメンテーションコメントを付与することで、
リクエストに対してバリデーションを行うことができる。

### バリデーションルールの定義

ファンクションコンテナのトップレベルに変数を定義し、ルールをオブジェクトにて格納する。

```js
let validationSetting = {
    family_name: {
        caption: "姓",
        required: true,
    },
    age: {
        caption: "年齢",
        number: true,
    },
};
```

### バリデーションルールの適用

ファンクションコンテナにドキュメンテーションコメントを付与する。ドキュメンテーションコメントを付与した関数は、バリデーションOKの場合に呼び出される。バリデーションNGの場合にはドキュメンテーションコメントを付与した関数は呼び出されず、`@onerror`アノテーションに指定した関数が代わりに呼び出される。
`@validate`アノテーションには、定義したバリデーションルールを指定する。
`@onerror`アノテーションには、バリデーションNG時に呼び出される関数を指定する。

```js
/**
 * クライアントから呼び出される任意の関数
 * @param {*} request 
 * @validate validation/validationSettings#validationSetting
 * @onerror onErrorSampleFunction
 */
function callByUserSampleFunction(request) {
    /* ... バリデーションOKの場合に行われる処理 ... */
}

/**
 * バリデーションNGの場合にintra-martから呼び出される関数
 */
function onErrorSampleFunction(request) {
    /* ... バリデーションNGの場合に行われる処理 ... */
}
```

### カスタムバリデーションの作成

#### 設定ファイルの配置

`WEB-INF\conf\jssp-validation-config`フォルダ内に`xml`ファイルを配置する。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jssp-validation-config xmlns="http://intra-mart.co.jp/system/jssp-validation"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://intra-mart.co.jp/system/jssp-validation ../../schema/jssp-validation-config.xsd">

  <!-- カスタムバリデーションサンプル（入力文字種：半角） -->
  <validator>
    <validator-name>custom_narrow</validator-name>
    <validator-script>customValidations/validation_narrow</validator-script>
  </validator>
  <!-- カスタムバリデーションサンプル（文字列バイト数） -->
  <validator>
    <validator-name>custom_existsMaster</validator-name>
    <validator-script>customValidations/validation_existsMaster</validator-script>
  </validator>
</jssp-validation-config>
```

`validator-name`属性には、バリデーションルール定義時に使用する名前を指定する。
`validator-script`はカスタムバリデーションの処理を記述したファイルを指定する。拡張子（.js）は含めない。

#### カスタムバリデーションの処理を記述

```js
/**
 * バリデーション実行
 * @param {Object} request クライアントからのリクエスト
 * @param {Object} config ルール定義のオブジェクト
 * @param {String} paramName パラメータ名
 * @param {String} caption 項目名称
 * @returns 
 */
function validate(request, config, paramName, caption) {
    /* ... バリデーション処理を記述する ... */
    // 検証OKの場合
    return {
        isValid: true,
        message: null,
    };
    // 検証NGの場合
    return {
        isValid: false,
        message: caption + "は半角を入力してください。",
    };
}
```

関数名を`validate`とする、4つに引数を受ける関数を定義する。
戻り値は`Object`を返却する。`isValid`プロパティは検証結果をbooleanで格納する。
検証NGの場合`message`にエラーメッセージを格納する。`caption`に項目名称が格納されている。

## クライアントサイドバリデーション

jQuery Validationをベースにintra-mart独自の拡張がされている。

### バリデーションルールの定義

ファンクションコンテナのトップレベルに変数を定義し、ルールをオブジェクトにて格納する。

```js
let validation = {
    // サンプル //
    ElementName: {
        caption: "エラーメッセージ",
        maxlength: 300 // サンプル // 最大文字数を指定する
    }
};
```

### バリデーションルールの適用

`imart`タグの`type`属性に`imuiValidationRule`を指定する。

```html
<imart type="imuiValidationRule" rule="SCRIPT_PATH#VARIABLE_NAME" rulesName="validationRulesName" messagesName="validationMessagesName" />
```

`rule`属性は`SCRIPT_PATH`部分にファンクションコンテナのパスを指定し、`VARIABLE_NAME`にファンクションコンテナ内でルールオブジェクトを定義した変数の名前を指定する。
`rulesName`属性に指定した名前でルールを格納したオブジェクトが作成される。
`messagesName`属性に指定した名前でメッセージを格納したオブジェクトが作成される。


### クライアントサイドでのバリデーションルール追加

`imuiValidationRule`関数でルールを追加することができる。

```js
// クライアントサイド バリデーションルール追加
imuiAddValidationRule(RULE_NAME, RULE_FUNCTION);
// クライアントサイド バリデーションメッセージ追加
MESSAGE_OBJECT.RULE_NAME = MESSAGE_TEXT;
// クライアントサイド バリデーション対象項目へのバリデーションルール設定
RULE_OBJECT.ITEM_NAME.RULE_NAME = RULE_ARGUMENT;
```

`imuiAddValidationRule`関数の引数にルール名と検証用の関数を設定し、バリデーションルールを追加する。<br/>
メッセージオブジェクトにプロパティを追加する。このとき、プロパティ名はルール名と同一とする。プロパティの値として検証エラー時のメッセージを設定する。<br/>
ルールオブジェクトにプロパティを追加する。このとき、プロパティ名は検証対象の`input`要素の`name`属性の値を設定する。

### チェックボックスがオンの場合のみ必須とする
バリデーションルール`required`の設定値にセレクタを指定すると、合致する要素が存在する場合に必須チェックが行われる。

```js
let validateRule = {
    ITEM_NAME : {
        caption   : MESSAGET_TEXT,
        required  : "#ITEM_ID:checked" // id属性がITEM_IDである要素がチェックされている場合にITEM_NAME項目を必須とする。
    },
};
```

## ルーティング

`WEB-INF/conf/routing-jssp-config`の配下に設定ファイルを配置する。
変更の反映には再起動が必要。
`file-mapping`要素にページのパスとテンプレートのパスのマッピングを記述し、
`authz-default`要素および`authz`要素に認可設定を記述する。

### file-mapping要素

`path`属性にページのパスを記述する。
`page`属性にテンプレートのパスを記述する。
テンプレートのパスは`WEB-INF/jssp/src`以降を記述する。
拡張子は記述に含めない。

### authz-default要素

デフォルトの認可設定を記述する。

### authz要素

ルーティングに対応するリソースURIを設定する。
ユーザーがURLにアクセスすると、対応するリソースURIの認可設定によりアクセスの可否が判断される。

### 資料

[intra-mart Accel Platform スクリプト開発モデル プログラミングガイド - ルーティング](https://document.intra-mart.jp/library/iap/public/development/script_programming_guide/texts/application/router/index.html#%E8%AA%8D%E5%8F%AF)<br/>

## ログ

`WEB-INF/conf/log`の配下に設定ファイルを配置する。
設定内容は`logback`に準ずる様子。

## 日付と文字列の相互変換

`DateTimeFormatter`オブジェクトを利用する。

参照: [DateTimeFormatterオブジェクト - スクリプト開発向けim-BizAPI](https://api.intra-mart.jp/iap/apilist-ssjs/doc/tenant/DateTimeFormatter/index.html)

## IM-Workflowの色々なコンテンツ画面へ遷移するURL

参照: [IM-Workflowの色々なコンテンツ画面へ遷移するURL - intra-mart Developer Site](https://dev.intra-mart.jp/cookbook176038/)
