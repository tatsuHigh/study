# Next.js

Next.js( React + Typescript )での環境を想定する

# プロジェクトのフォルダ構成

Next.js では以下の 2 フォルダだけ特別な意味を持つフォルダとして扱われる

## pages

\*\*/pages 配下に置かれたファイルは自動ルーティングされる  
ex) ドメインが`http://sample.com`の場合  
・pages/index.tsx  
→`http://sample.com`でアクセス可能  
・pages/abc.tsx  
→`http://sample.com/abc`でアクセス可能  
・pages/dir1/index.tsx  
→`http://sample.com/dir1`でアクセス可能  
・pages/dir1/abc.tsx  
→`http://sample.com/dir1/abc`でアクセス可能  
※index.tsx は特別扱いされる

## public

public 配下に画像を置くと、以下のようにアクセスできるようになる  
ex) favicon.ico を public/favicon.ico に設置した場合  
`ドメイン.com/favicon.ico`でアクセス可能

# レンダリング方法

Next.js ではページ毎にレンダリング方法を変えることができ、以下の 3 つの方法がある

## CSR

クライアントサイドレンダリング。  
特に何もしなければこの形式になる。

## SSR

サーバーサイドレンダリング。  
以下のように`getServerSideProps`メソッドの記述を tsx ファイル内にすることで、そのメソッド内の処理は SSR される。

```
export async function getServerSideProps(context) {
  return {
    props: {
      // コンポーネントに渡すための props
    }
  }
}
```

## SSG

静的生成。  
以下のように`getStaticProps`メソッドの記述を tsx ファイル内にすることで、そのメソッド内の処理は SSG される。

```
export async function getStaticProps() {
  const allPostsData = getSortedPostsData()
  return {
    props: {
      allPostsData
    }
  }
}
```
