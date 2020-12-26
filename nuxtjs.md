# Nuxt.js
Nuxt.js( Vue.js + Express + Typescript )での環境を想定する

# VueへTypescritを適用
```
<script lang="ts">
```
とする

# ライフサイクルフック
決まった名称のメソッドを定義することで、Vueのライフサイクルにあった部分での処理を書くことができる
```
// コンポーネントがマウントされた時の処理
mounted(){

}

// コンポーネントが破棄される直前の処理
beforeDestroy(){

}
```

# コンポーネントの定義
定義方法
```
@Component
export class SampleComponent extends Vue{}
```
引数
```
@Component({
    // 他コンポーネントの取り込み
    components:{
        AppButton,
    },
    // レイアウトの使用
    layout: 'sample',
    // computedにmapGettersの中身を展開し、このコンポーネント内で使えるようにする
    computed:{
        ...mapGetters({
            gettername: 'sample/gettername'
        })
    },
})
export class SampleComponent extends Vue{
    // getterをscript内で使いたい場合は同じ名前の変数を定義する
    gettername: any

    // this.getternameでアクセス
}
```

# Data
dataはクラスのメンバーとして定義することで利用できる
```
@Component
export class SampleComponent extends Vue{
    name: string = 'name'
    age: number = 25
}
```

# Methods
関係ない部分の更新でも再計算される
```
methodname(){
    // 単純なメソッド定義で実現可能
}
```

# Computed
関係のある時だけ再計算される
```
get methodname(){
    // getterにすることで実現可能
}
```

# @Prop
※Vuexを使用するならあまり使うことはない
コンポーネント間でデータのinputをする。
コンポーネントにpropsを指定すると、そのコンポーネントを利用するときにpropsに指定した属性を記述することができ、親から値を受け取って子のテンプレート内に値を受け渡すことができる。
```
export class SampleComponent extends Vue {
    @Prop({ type: String, required: true})
    userName: string
}
```

# @Emit
※Vuexを使用するならあまり使うことはない
コンポーネント間でデータのoutputをする。
以下のようにすると、子コンポーネントに置かれたbuttonクリックで親のcallが呼ばれる。
```
◆Parent.vue
<template>
    <div>
        <Child @calledChild="call()" />
        <p>{{ phrase }}</p>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"
import { Child } from "./Child.vue"
@Component({
    components:{
        Child
    }
})
export class Parent extends Vue {
    public phrase: string = "無音"
    public call(){
        this.phrase = "おーい"
    }
}
</script>
```
```
◆Child.vue
<template>
    <div>
        <button @click="calledChild()">呼ぶ</button>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Emit } from "vue-property-decorator"
@Component
export class Child extends Vue {
    @Emit()
    public calledChild(){}
}
</script>
```

# @Watch
第一引数に監視したい値へのパスを、第二引数にウォッチャのオプションを設定
immediate: trueはコンポーネント初期化時にも処理を実行するか 
```
@Watch('profile.age', { immediate: true })
onChangeProfileAge() {
    // プロフィールの年齢が変更された時の処理
}
```

# getter, setterとメソッドの違い
getter, setterはプロパティと同様なアクセスできる
```
get getter(): string{}
→ const a = getter

set setter(b: string){
    this.b = b
}
→ setter = b
```

# Typescriptでのenum
Typescriptでは以下の理由からenumではなくunionを使うべき
・反復処理が可能
・JavaScriptにトランスパイルしてもIIFEが生成されないのでTree-shaking不可能
※Tree-shakingとはバンドル時に不要なコードを削除する機能

# Vuex(Typescript + vuex-module-decorators)
◆State  
クラスのプロパティとして定義  

◆Mutation  
@Mutationをつける  
Mutationwo通してしかStateを変更してはいけない  

◆Action  
@Actionをつける  
非同期処理をする際はActionを経由してMutationにアクセスする

◆Getter  
getterとして定義する  
Stateのアクセサ  

◆Vuexの流れ(小文字は呼び出すために使用するメソッド)  
Components→dispatch→Actions→commit→Mutations→mutate→State→render→Components  
※基本コンポーネントから直接Mutationを呼び出すより、Actionを経由してMutationを呼び出すのがいいらしい。個人的には非同期じゃなければ直接Mutationを呼んでもいいと思う。

◆配列やオブジェクトの変更見地について  
vuexでの配列やオブジェクトは変更されたかを認識するのに条件がある  
例えば配列で言うと、配列を丸ごと入れ替えたら変更とみなされないため、pushなどを行う必要がある。

# Express
◆app.getとrouter.getの違い  
app.getをモジュール化したものがrouter.get  
app.useはモジュール化したものを読み込む  
router.routeでパスを指定した後、続けて.get.postなど、同じパスをメソッド違いで続けることができる

# Typescript 環境変数
以下で環境変数にアクセスできる
```
process.env.環境変数名
```
接続DB情報などを環境変数経由で取得するのが望ましい  
.envファイルを使って環境変数を設定してもよい

# Typescript 関数定義方法
```
// アロー関数式 ※これだけ覚えておけばよい
const func = (arg: string) => arg

// 名前付き関数
function func (arg: string) {
    return arg
}

// 関数式
const func = function(arg: string) {
    return arg
}
```