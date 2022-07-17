## Slack Events取得サーバー立ち上げ手順
### ① 環境変数設定
```sh
export V_TOKEN="your Verification Token "
```

Verification Tokenは以下で取得
SlackApp管理画面 > Basic Information > App Credentials 

### ② サーバー立ち上げ
```sh
go build main.go
./main
```

### ③ ローカルサーバーを外部に公開
ローカルで立てたサーバーを外部公開するのにngrokを利用する。
```  
brew install ngrok/ngrok/ngrok
ngrok http 3000 
```

### ④外部公開されたURI取得
③のコマンドを実行すると、https://xxxxxxxxx-xxxxxxxxxxx-xx.jp.ngrok.io のようなURIが発行される。
以下が、eventを受け取るエンドポイントになる。
https://xxxxxxxxx-xxxxxxxxxxx-xx.jp.ngrok.io/events-endpoint　

### ⑤slack管理画面からURL登録
④で取得したエンドポイントを、slackに登録する。
以下から、Enable Events をon にし、Request URLに貼り付け。
SlackApp管理画面 > Event Subscriptions

権限は、Subscribe to events on behalf of users に任意のものを設定。

Subscribe to bot eventsは、botが入っている部屋しかイベント対象にならない。

### ⑥リクエスト取得
slackで任意のeventsを起こすと、標準出力にbodyが出力される。