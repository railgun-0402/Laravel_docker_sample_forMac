##環境
- 動作環境  
macOS Catalina 10.15.1
- 開発環境  
php 7.x  
laravel 6.x
##構築手順
###1. プロジェクトディレクトリの作成
```
$ mkdir project-name
$ cd project-name
```
*project-nameは任意

###2. 環境に合わせてポートを修正
docker-compose.ymlで下記の箇所を環境に合わせて修正します。
8行目 Webアクセス用ポート
10080:80
27行目 DBアクセス用ポート
13306:3306

###3. Docker環境を構築する
```
$ docker-compose build
```

###4. Docker環境を起動する
```
$ docker-compose up -d
```

###5. Docker環境に入る
```
$ docker-compose exec php bash
```

###6. Laravelプロジェクトを作成する
```
/src# laravel new project-name
```
*project-nameは任意

###7. ちょっと小細工...
/src/project-name/以下にlaravelが構築されますので、階層を1つ上へ移動します。
```
/src# mv project-name/* .
/src# mv project-name/.[^\.]* .
/src# rm -Rf project-name
```
これでsrc以下にlaravelのファイルが移動しました。

###8. laravelのDB接続設定
.envファイルをdocker-compose.ymlのmysqlセクションを参考に修正します。
```
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel-project-db
DB_USERNAME=root
DB_PASSWORD=root
```

###9. データベースのマイグレーション
```
/src# php artisan migrate
```

###laravelの動作確認
ブラウザで http://localhost:10080 へアクセスしlaravelの初期ページが表示されれば、ひとまず環境構築は完了です。
お疲れ様でした。

###データベースに直接接続する
Mysql workbenchなどでdockerで起動したmysqlへ接続する場合は以下の設定で接続できます。
ホスト　0.0.0.0
ポート　13306
ユーザー名　root
パスワード　root
