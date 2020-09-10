## Maven
### 実行方法
cmdを開き、pom.xmlがあるフォルダに移動してからmvnコマンドを実行する。

### テストクラスを指定してテスト
```mvn test -Dtest=テストクラス名```

### Eclipseでmaven指定jarと同じプロジェクトがインポートされている場合
jarのclassではなくjavaファイルを参照してしまう
→プロジェクトを閉じることでjarファイル内のclassを参照する