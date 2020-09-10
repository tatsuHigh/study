## Docker
### dockerイメージの作り方
1. Dockerfileを作成する
    Dockerfile中身例
    FROM 元にするイメージ
    COPY test.txt /app
2. Dockerfileがあるフォルダに移動し、以下コマンドを打つ ※.の前に半角スペース有り
```docker build -t イメージ名:タグ名 .```
3. 以下コマンドで作成されているか確認
```docker images```

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

