## Elasticsearch
### クライアントソフト
chromeの拡張機能「elasticsearch head」

### 基本コマンド
#### mapping.jsonの取得
```
curl -s -X GET "http://localhost:9200/インデックス名/_mapping?prentty" > C:\Users\User1\Desktop\test.json
```
#### index作成
```
curl -X PUT -H "Content-Type: application/json" "http://localhost:9200/インデックス名" --data-binary @json名
```
#### index削除
```curl -XDELETE http://localhost:9200/インデックス名```