## Maven
### 実行方法
cmdを開き、pom.xmlがあるフォルダに移動してからmvnコマンドを実行する。

### 基本コマンド
#### target配下初期化
```mvn clean```
#### 全体テスト
```mvn test -Dmaven.test.failure.ignore=true > C:\Users\User1\Desktop\log.txt```
#### テストクラスを指定してテスト
```mvn test -Dtest=テストクラス名```
#### htmlレポート出力
```mvn site -Dmaven.javadoc.failOnError=false -Dmaven.test.skip=true -Dcheckstyle.skip```

### Eclipseでmaven指定jarと同じプロジェクトがインポートされている場合
jarのclassではなくjavaファイルを参照してしまう
→プロジェクトを閉じることでjarファイル内のclassを参照する