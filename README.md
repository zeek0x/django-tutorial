# [はじめての Django アプリ作成](https://docs.djangoproject.com/ja/3.0/intro/tutorial01/)

# Notes
## ディレクトリ構造
以下のコマンドをコードの保存場所で実行することにより Django project が生成される
```console
$ django-admin startproject mysite
```

生成されるファイル群
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

- mysite(root): 名前が意味を持たないルートディレクトリ。本来の Django プロジェクトでは、レポジトリのディレクトリにするのが一般的なようだ
- manage.py： Django project のコマンドランユーティリティ `pythoh3 manage.py $command` の形で実行
  - `python3 manage.py runserver`：開発用サーバ起動
  - `python3 manage.py shell`：Django project 環境でREPL起動
  - `python3 manage.py test`：テスト実行
  - etc...
- __init__.py: -
- settings.py: Django project の設定ファイル
- urls.py: ルーティングを記述
- asgi.py: ASGI互換Webサーバのエントリ
- wsgi.py: WSGI互換Webサーバのエントリ


## プロジェクトとアプリケーション

> プロジェクトとアプリの違いは何でしょうか？ アプリとは、ウェブログシステム、公的記録のデータベース、小規模な投票アプリなど、何かを行う Web アプリケーションです。プロジェクトは、特定のウェブサイトの構成とアプリのコレクションです。プロジェクトには複数のアプリを含めることができます。 アプリは複数のプロジェクトに存在できます。

うまく作らないと簡単にプロジェクトに依存しそう（初並感）
> Django アプリケーションは「プラガブル (pluggable)」です。アプリケーショ ンは特定の Django インストールに結び付いていないので、アプリケーションを複数のプロジェクトで使ったり、単体で配布したりできます。

プロジェクトとアプリは多対多の関係

Django アプリの作成
```
$ python manage.py startapp polls
```

以下のファイル群が生成
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

## settings.py
### DATABASES
- Engine
- DB アクセスに必要な設定

### INSTALLED_APPS
デフォルト
> django.contrib.admin - 管理（admin）サイト。まもなく使います
django.contrib.auth - 認証システム
django.contrib.contenttypes - コンテンツタイプフレームワーク
django.contrib.sessions - セッションフレームワーク
django.contrib.messages - メッセージフレームワーク
django.contrib.staticfiles - 静的ファイルの管理フレームワーク

migrate を実行する前なら settings.py から削除できる。
migrate は INSTALLED_APPS のために実行される。

#### migrate
INSTALLED_APPS がデータベースを使用するためにテーブルを作成する
```
python manage.py migrate
```


> migrate コマンドは INSTALLED_APPS の設定を参照するとともに、 mysite/settings.py ファイルのデータベース設定に従って必要なすべてのデータベースのテーブルを作成します。このデータベースマイグレーションはアプリと共に配布されます (これらについては後ほどカバーします)。マイグレーションを実施
するたび、メッセージを見ることになります。

データベースマイグレーション：テーブル操作。マイグレーションを行う

INSTALLED_APPS に polls を追加して下記コマンドを実行
```
$ python manage.py makemigrations polls
```

`sqlmigrate` はマイグレーションの中身のテーブル操作を知ることができる
```
$ python manage.py sqlmigrate polls 0001
```

## Django Admin
管理ユーザーを作成するとともに、admin サイトに入れるようになる
```
$ python manage.py createsuperuser
```

## Templates
Django は、アプリのサブディレクトリ `templates` のサブディレクトリを探索する。

めっちゃくちゃびみょいのだが、名前空間を分けるために `templates/polls` を掘る必要があるらしい...
```
polls/templates/polls/index.html
```

## URL の名前空間
project の urls.py で評価されたあと、マッチした各 app の urls.py で評価される

`/polls/5/` の場合、 mysite/urls.py で `polls/` がマッチして、それを取り除き、残りの文字列である `5/` を polls/urls.py に渡す
