# [はじめての Django アプリ作成](https://docs.djangoproject.com/ja/3.0/intro/tutorial01/)

## Notes
### ディレクトリ構造
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
- __init__.py: -
- settings.py: Django project の設定ファイル
- urls.py: ルーティングを記述
- asgi.py: ASGI互換Webサーバのエントリ
- wsgi.py: WSGI互換Webサーバのエントリ


### プロジェクトとアプリケーション

>>> プロジェクトとアプリの違いは何でしょうか？ アプリとは、ウェブログシステム、公的記録のデータベース、小規模な投票アプリなど、何かを行う Web アプリケーションです。プロジェクトは、特定のウェブサイトの構成とアプリのコレクションです。プロジェクトには複数のアプリを含めることができます。 アプリは複数のプロジェクトに存在できます。

プロジェクトとアプリは多対多の関係
