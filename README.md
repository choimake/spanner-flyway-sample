# spanner-flyway-sample
Spannerエミュレータとflywayを連携させたサンプル


## 環境構築手順

### コンテナの立ち上げ
以下コマンドを実行
```
docker-compose up -d
```

### ローカルマシンのgcloud configを設定する（エミュレータの動作確認用）
```
gcloud config configurations create emulator
gcloud config set auth/disable_credentials true
gcloud config set project test-project
gcloud config set api_endpoint_overrides/spanner http://localhost:9020/
```

作成したデータベースにクエリを発行し、エラーがなければ成功
```
gcloud spanner databases execute-sql test-database --instance test-instance --sql="SELECT 1"
```

## flywayでのmigrate実行コマンド
```
docker-compose run --rm flyway migrate
```

テーブルが追加されていれば成功
