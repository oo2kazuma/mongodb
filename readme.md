
RDBエンジニアでもできる！MongoDBの構築と運用入門（目黒 聖）の環境をdocker-composeで再現。
forkする関係でPID1プロセスはtailだったり、本書を忠実（systemdの未使用）に再現していなかったりです。

# 前提
docker-composeが実行できる環境であること

# コマンド
# 起動
docker-compose up

# 停止
docker-compose down

# tips
# dockerfileを編集したときdockerイメージのキャッシュが残る場合がある
dockerfile変更時にビルドが走るようにオプション付き
docker-compose up --build

