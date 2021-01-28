# Next.js

Next.js は React のフレームワーク  
(React は JavaScript のフレームワーク。フレームワークのフレームワークなので混乱してしまうが、React 以外にも開発に役立つライブラリなどがパッケージングされているものだと思うといいかも)

本説明では Next.js( React + Typescript )での環境を想定する

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
そのほか、ダイナミックルーティングと呼ばれるものもある(公式を参照)。

公式：https://nextjs.org/docs/basic-features/pages

## public

public 配下に画像を置くと、以下のようにアクセスできるようになる  
ex) favicon.ico を public/favicon.ico に設置した場合  
`ドメイン.com/favicon.ico`でアクセス可能

# 特別なクラス

Next.js では特別な意味を持つフォルダがあるように、特別な意味を持つクラスも存在する。

## \_app.tsx

pages 配下に存在するクラス。
一言でいうと全ページ共通で必要な処理を定義することができる  
例）  
・グローバル CSS を定義できる  
・共通 state を定義できる  
・ページ間共通レイアウトを定義できる
等

## \_document.tsx

pages 配下に作成するべきクラス(作らなくても動くが細かい設定が必要なら作った方がいい)。
SSR 時の全体の文書構造を設定するためのクラス

# コンポーネントの作成方法

コンポーネントの作成方法は 2 通りある
新しい書き方である関数コンポーネントが推奨される(書き方がシンプルだしパフォーマンスもよい)

## 関数コンポーネント

```
import * as React from 'react'

const Sample = () => {
  const message = '関数コンポーネントです'
  return (
    <div>
      <p>{ message }</p>
    </div>
  )
}
export default Sample
```

## クラスコンポーネント

```
import * as React from 'react'

class Sample extends React.Component {
 constructor(props) {
   super(props);
   this.state = {
     message: 'クラスコンポーネントです'
   };
 }
 render() {
   return (
     <>
       { message }
     </>
   );
 }
}
export default Sample
```

# React hooks

React hooks は簡単に言うと、

「関数コンポーネントはシンプルだしパフォーマンスもいいから使いたい！けど、クラスコンポーネントで実現できていたことの一部が実現できないので、関数コンポーネントでも実現できるように後付けで作られたもの」

って感じ。  
なので関数コンポーネントのためにあるもの。

```
useState
useEffect
```

などがある。

参考：https://qiita.com/seira/items/f063e262b1d57d7e78b4
公式：https://ja.reactjs.org/docs/hooks-reference.html

# レンダリング方法

Next.js ではページ毎にレンダリング方法を変えることができ、以下の 3 つの方法がある  
レンダリングはページの生成方法であり、API の呼び出し方法とは別。  
React コンポーネントから直接 API を呼ぶ方法はクライアントフェッチと呼ぶ。  
※`getInitialProps`は昔の記法のため、下記推奨

## CSR（Client Side Rendering）

静的なファイルを返す。  
特に何もしなければこの形式になる。

## SSR（Server Side Rendering）

リクエスト時にサーバーサイドでページをレンダリングして返す。  
以下のように`getServerSideProps`メソッドの記述を tsx ファイル内にすることで、そのメソッド内の処理は SSR 時に実行される。

```
import { GetServerSideProps } from 'next'

export const getServerSideProps: GetServerSideProps = async (context) => {
  return {
    props: {
      // コンポーネントに渡すための props
    }
  }
}
```

## SSG（Static Site Generation）

ビルド時にサーバーサイドでページをレンダリングし、静的ファイルとしてウェブサーバーに持っておく。  
リクエスト時には静的なファイルを返す。  
以下のように`getStaticProps`メソッドの記述を tsx ファイル内にすることで、そのメソッド内の処理は SSG 時に実行される。

```
import { GetStaticProps } from 'next'

export const getStaticProps: GetStaticProps = async (context) => {
  const allPostsData = getSortedPostsData()
  return {
    props: {
      allPostsData
    }
  }
}
```

公式：https://nextjs.org/docs/basic-features/typescript#static-generation-and-server-side-rendering
