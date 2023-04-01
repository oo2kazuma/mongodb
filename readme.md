
RDBエンジニアでもできる！MongoDBの構築と運用入門（目黒 聖）の環境をdocker-composeで再現。
forkする関係でPID1プロセスはtailだったり、本書を忠実（systemdの未使用）に再現していなかったりです。
mongo6もポート違い（27018）で利用できます。

# 前提
docker-composeが実行できる環境であること

# 注意
adminユーザは作られていません。リスト4.5を実施してください。

# コマンド
# 起動
docker-compose up

# 停止
docker-compose down

# tips
# dockerfileを編集したときdockerイメージのキャッシュが残る場合がある
dockerfile変更時にビルドが走るようにオプション付き
docker-compose up --build

#コマンド
db.createUser(
    {
        user: "admin",
        pwd: "password",
            roles:[{ role:"root", db:"admin"}]
    }
)

db.dropDatabase()

db.createUser({ user: "testdbOwner",pwd: "password", roles:[{ role:"dbOwner", db:"testdb"}]})


db.changeUserPassword("testdbOwner","yuruora")

db.dropUser("testdbOwner")

db.createCollection("testcollection")

show collections

db.createCollection( "log", { capped: true, size: 1048576})
db.createCollection( "log3", { capped: true, size: 1048576, max: 10000})

db.createCollection( "log2", { capped: true, max: 10000})

db.createCollection("fishes")

db.fishes.find()

■リスト6.5
db.createCollection("attrival")
db.attrival.insert(
    {
        arrivalDate: ISODate("2021-06-04T10:00:00+09:00"),
        fishes: [
            {name: "サンマ", price: 360},
            {name: "タイ", price: 500},
            {name: "サバ", price: 400}
        ],
        notes: null
    }
)

db.fishes.find({},{_id:0})

db.fishes.find({ name: "マグロ"},{_id:0})

db.fishes.find({ name: /サ/},{_id:0})

db.fishes.find({ "price": { $gte: 300, $lt: 500}},{_id:0})

db.fishes.find(
    { $and: [
        { "name": /サ/},
        {"price": { $gte: 300}}
        ]},
        {_id:0})