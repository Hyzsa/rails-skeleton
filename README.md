# rails-skeleton

## 概要
rails7 + PostgreSQLのdocker開発環境構築用のスケルトンです。

## 構築手順
1. `rails new`する。
```docker
docker compose run web rails new . --force --database=postgresql
```

2. Gemfielが更新されているので`bundle install`する。
```docker
docker compose build
```

3. DBの接続設定を行うため`src/config/database.yml`の内容を以下で上書きする。
```ruby:database.yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test
```

4. DBを作成する。
```docker
docker compose run web rails db:create
```

5. コンテナを起動する。
```docker
docker compose up -d
```

6. ブラウザで http://localhost:4000/ にアクセスして、Railsが立ち上がっていれば成功！
