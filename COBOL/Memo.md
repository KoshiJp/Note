# COBOL

## プログラムの構成

IDENTIFICATION DIVISION（見出し部）：します123。
ENVIRONMENT DIVISION（環境部）：します。これには、ファイルの入出力や、コンピュータの設定などが含まれます123。
DATA DIVISION（データ部）：ます123。
PROCEDURE DIVISION（手続き部）：プログラムの主要な処理を記述します。ここには、算術演算、条件分岐、ループなどの手続きが含まれます123。

### IDENTIFICATION DIVISION - 見出し部

プログラムの名前やバージョン、著者など、プログラムの識別情報を記述する。

### ENVIRONMENT DIVISION - 環境部

プログラムが動作する環境に関する情報を記述する。コンピュータの設定などが含まれる。

- CONFIGURATION SECTION
  - SOURCE-COMPUTER 翻訳するコンピューター
  - OBJECT-COMPUTER 実行するコンピューター
- INPUT-OUTPUT SECTION
  - FILE-CONTROL ファイル管理

### DATA DIVISION - データ部

プログラムで使用するデータ項目の定義を行う。

- FILE SECTION ファイル
- WORKING-STORAGE SECTION 作業領域
- LINKAGE SECTION 外部連携
- COMMUNICATION-SECTION 通信
- REPORT SECTION レポート

### PROCEDURE DIVISION - 手続き部

プログラムの主要な処理を記述する。算術演算、条件分岐、ループなどの手続きが含まれる。

## プログラムのフォーマット

1行 = 一連番号領域 + 標識領域 + A領域 + B領域 + 見出し領域

### 一連番号領域

1～6文字目。
6桁の行番号。

### 標識領域

7文字目。行の区分を示す。

- 空白 プログラム行を示す。
- `*` コメント行を示す。
- `-` 前の行から継続する行を示す。

### A領域

8～11文字目。

### B領域

12～72文字目。

### 見出し領域

73～80文字目。

## 命令文

### DISPLAY

```COBOL
DISPLAY <TEXT> UPON <DESTINASTION>.
```

- TEXT 出力内容
- DESTINASTION CONSOLE | SYSOUT 出力先。コンソール、または標準出力。

### ACCEPT

```COBOL
ACCEPT <VARIABLE> UPON <SOURCE>.
```

- VARIABLE 入力データを格納する変数。
- SOURCE 入力元。

### IF-THEN

