## Docker
### dockerイメージの作り方
1. Dockerfileを作成する
    Dockerfile中身例
    FROM 元にするイメージ
    COPY test.txt /app
2. Dockerfileがあるフォルダに移動し、以下コマンドを打つ ※.の前に半角スペース有り
```docker build -t イメージ名:タグ名 .```

### dockerイメージ一覧
```docker images```

### 起動中コンテナ一覧
```docker ps```  
※NAMESカラムがコンテナ名

### コンテナの起動
```docker start コンテナ名```

### コンテナの停止
```docker stop コンテナ名```

### コンテナのbashにログイン
```docker exec -it コンテナ名 bash```

### コンテナのログをリアルタイムで確認
```docker logs -f コンテナ名```

### ホスト→コンテナ、コンテナ→ホストへファイルコピー
```
docker cp ファイルパス コンテナ名:ファイルパス
ex) docker cp C:\Users\User1\Desktop\test.txt コンテナ名:/app/test.txt
```

### コンテナのCPU,Memory使用状況確認
```docker stats```

## Docker Hub
※Dockerイメージの管理ができるWebアプリケーション
### docker hubへのログイン
```docker login```
ユーザー名、パスワードを入力する

### dockerイメージを取得する
```docker pull イメージ名```

### dockerイメージをcommitする
```docker commit コンテナ名 アカウント名/リポジトリ名```

### dockerイメージをpushする
```docker push アカウント名/リポジトリ名:タグ名```

## Docker Compose
※複数のコンテナを一気に実行できるツール