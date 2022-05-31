# FTP / メモ

## FTPコマンド

### サーバーへ接続する

```
open <ip-address>
```

### 接続を切断する

```
bye
```

### ログイン

```
user <user-name> <password>
```

### ファイルの一覧を表示する

```
ls
```

### ディレクトリの一覧を表示する
```
dir
```
### ファイルをダウンロードする

```
get <server-file> <client-path>
```

### サーバーで実行されるコマンドを送信する

```
quote <command-string>
```
`command-string`をサーバーへ送信する。サーバーがコマンドを解釈し実行する。スペースで区切ることで引数を指定することもできる。