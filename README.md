# stock_trader

Udemy の [Vue JS 2 - The Complete Guide (incl. Vue Router & Vuex)](https://www.udemy.com/course/vuejs-2-the-complete-guide/) 教材で作成した株式トレーダーアプリです  
アプリの作成後、Docker化して開発がしやすいようにカスタマイズしています

![00_stock_trader](https://raw.githubusercontent.com/dodonki1223/image_garage/master/stock_trader/00_stock_trader.gif)

## 環境

環境については以下の通りである

| 環境         | バージョン  |
|:-------------|:-----------:|
| Node.js      | 12.16.3     |
| Vue.js       | 2.6.11      |
| Vuex         | 3.5.1       |
| vue-router   | 3.3.4       |
| vue-resource | 1.5.1       |

### vue-resourceについて

以前までは公式の推奨のものだったが、現在は非推奨になっています  
今後は [Axios](https://github.com/axios/axios) を使用することをオススメします

詳しくはこちら [vue-resource の引退について — Vue.js](https://jp.vuejs.org/2016/11/03/retiring-vue-resource/) を参照してください

### バージョンの確認方法

バージョンの確認方法は以下を実施

#### Node.js

```shell
$ node -v
```

#### npmモジュールの確認方法

```shell
$ npm list module_name
```

## 開発

基本的にdockerを使用して開発を行います  
開発用に `stock_trader`、`runner` の2つのサービスを作成しているのでこの2つのサービスを使用して開発を行っていきます  
またデータベースは [Firebase](https://console.firebase.google.com/u/0/?hl=ja) を使用しているので [Firebase](https://console.firebase.google.com/u/0/?hl=ja) の設定を行う必要があります

### Firebase設定

> ./src/main.js

のファイル内の `Vue.http.options.root = 'https://sample.firebaseio.com/';` のURLにFirebaseで使用する Realtime Database のURLを設定してください

**本来なら.envファイルなどで管理するベきものだがなぜかうまく値を取得できなかったのでこういう形にしています**

### stock_traderを起動する

下記コマンドを実行後、[http://localhost:8080/](http://localhost:8080/) にアクセスしてください

```shell
$ docker-compose up stock_trader
```

### runnerを起動する

`npm i hogehoge --save` や `npm run lint` などのコマンドを実行するためのサービスになります

```shell
$ docker-compose run --rm runner
```

## その他

### 開発環境を削除する

コンテナ、イメージ、ボリューム、ネットワークをすべて一括で削除します

```shell
$ docker-compose down --rmi all --volumes
```

参考記事：[《滅びの呪文》Docker Composeで作ったコンテナ、イメージ、ボリューム、ネットワークを一括完全消去する便利コマンド - Qiita](https://qiita.com/suin/items/19d65e191b96a0079417)
