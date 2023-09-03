---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev

---
# VueとReact: ウェブ開発のための最初のステップ

Presentation slides for developers
<common-slide/>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# 目次

## Vue.jsについて

## Vue.js 2.0から3.0への移行

## サポート終了と意味

## Composition API

## Reactについて

## Reactの基本概念

## React vs Vueの比較

<common-slide/>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# vueとは？

Vue.jsは、Webインターフェースを構築するためのプログレッシブフレームワークです。重要な特徴の1つは、プログレッシブな採用が可能なことで、コアライブラリはビュー中心のアプリケーションに焦点を当てていますが、最新のツールやサポートするライブラリと組み合わせると、複雑なシングルページアプリケーションを簡単に構築することができます。

### history
- 2013年: Evan YouがVue.jsを初めて公開。 彼は以前AngularJSプロジェクトで働いており、Angularのコンセプトをよりシンプルにする目的でVueを開発することになりました。
- 2016年: Vue 2.0が発表され、このバージョンでは仮想DOM、サーバーサイドレンダリングなどの主要機能が導入されました。
- 2020年：Vue 3.0がリリースされ、Composition API、仮想DOMの改善、TypeScriptのサポート強化など、さまざまな新機能と最適化が行われました。

<br><br>

<common-slide/>


---
transition: fade-out
---
<!--
Here is another comment.
-->

# vue2.0のサポート終了とその意味 

### Vue 2.0のサポート終了：
- Vue 2.0の公式サポート終了は、Vue 3.0の安定リリースとともに開始されます。これは、開発者コミュニティにVue 3.0の新機能と最適化を採用することを推奨することを意味します。
- サポート終了は、セキュリティパッチとバグ修正が提供されなくなることを意味します。 したがって、既存のVue 2.0プロジェクトは、時間の経過とともにセキュリティと安定性の問題に直面する可能性があります。

### サポート終了の意味 
- アップグレードの必要性：Vue 2.0を使用するプロジェクトを維持・運営する開発者やチームは、徐々にVue 3.0への移行を検討する必要があります。
- 新機能: Vue 3.0は、**Composition API**、パフォーマンスの向上、ツリーシェイクのサポートなど、多くの新機能と改善点を提供します。これらの新機能はVue 2.0では利用できません。

<common-slide/>
---
transition: fade-out
---

# Vue2.0から3.0への移行 

## CompositionAPI
- Vue 3.0の一番大きな変化の一つはComposition APIの導入です。
- 以前のOptions APIはコンポーネントのロジックをオプション別に分離しましたが、Composition APIは機能別にロジックを再利用して構成することができます。
- これにより、コンポーネントの読みやすさと再利用性が向上しました。

<common-slide/>
---
transition: fade-out
---

# 既存のOptional APIとの比較 
<br>
<img src="https://velog.velcdn.com/images/buddle6091/post/a82ee5b3-8c6d-4a06-bacd-fb49d8b10f5c/image.png" style="width: 80%; height:80%;">


<br>
<common-slide/>

---
transition: fade-out
---

# 既存のOptional APIとの比較 
<br>

## Composition APIと再利用性
Composition APIはVue 3で導入された新しいAPIで、複雑なコンポーネントロジックを簡単に構成して再利用することができます。

- 問題点：
従来のOption APIのmixinsはロジックを再利用する方法の一つでしたが、衝突のリスク、ソースが不明瞭な属性など、様々な問題がありました。
- 解決：
Composition APIはreactiveとrefを使って反応性のあるデータを作って、setup()関数内でロジックを構成して問題を解決します。
カスタムフックを簡単に作成し、ロジックを再利用することができます。

<br><br>
<common-slide/>

---
transition: fade-out
---

# 既存のOptional APIとの比較 

### Mixin の使い方
```
const myMixin = {
  data() {
    return {
      message: "Hello from mixin!"
    };
  },
  created() {
    console.log(this.message);
  }
};
```
### Mixinを使う
```
new Vue({
  mixins: [myMixin],
  created() {
    console.log('Component created!');
  }
})

// Hello from mixin!
// Component created!
```
<br>
<common-slide/>

---
transition: fade-out
---

# 既存のOptional APIとの比較 

### Mixin の属性衝突

```
new Vue({
  mixins(ミクシィン)[myMixin]、
  data() {
    return {
      message: "Hello from component!"
    };
  }、
  created() {
    console.log(this.message);
  }
}).$mount("#app");
```
を実行すると 
```
Hello from component!
Hello from component!
```
- 両方の created フックが実行されますが、message データ属性の値はコンポーネントのものが mixin のものより優先的に使用されます。 そのため、"Hello from component!" が2回出力されます。
<br>
<common-slide/>

---
transition: fade-out
---

# 既存のOptional APIとの比較 
<br>

## 本格的なタイプ推論
Vue 3はTypescriptとの互換性が大幅に向上しました。
Options APIの場合も、TypeScript特有の型推論を実装するために非常に[非効率的な方法](https://github.com/vuejs/core/blob/44b95276f5c086e1d88fa3c686a5f39eb5bb7821/packages/runtime-core/src/componentPublicInstance.ts#L132-L165)を使っていると公式ドキュメントでは説明されています。

  - 特徴：
    Composition APIはタイプ推論を自動化するための構造を持ちます。
    Vue 3の内部コードもTypescriptで書かれているので、Typescriptとの統合がよりスムーズになりました。

## より小さな生産バンドルとより少ないオーバーヘッドの削減
- Vue 3は`<script setup>` タグを導入し、コンポーネントロジックをもっと簡潔に書くことができるようになりました。
- 特徴：
`<script setup>` を使うと、コンポーネントのテンプレートがコードと同じ範囲でインライン関数としてコンパイルされます。
これにより、既存のOption APIでthisを使用してデータにアクセスすることを減らすことができます。
変数名を安全に短縮できるため、バンドルサイズが小さくなり、パフォーマンスが向上します。

<br><br>
<common-slide/>

---
transition: fade-out
---

# Reactとは？

Reactはユーザーインターフェースを構築するためのJavaScriptライブラリです。主な特徴は、コンポーネントベースのアーキテクチャと仮想DOMを使用して効率的な更新とレンダリングを提供することです。


### history
- 2013年: FacebookがReactを公開します。元々はFacebookのニュースフィードに対するインタラクティブ性の向上を目的として開発されました。
- 2015年: React Nativeが発表され、モバイルアプリケーション開発にもReactが使えるようになりました。
- 2017年: React 16 (React Fiber)が発表され、このバージョンではコアアルゴリズムの完全な書き換えが行われました。
- 2019年: Hooksが導入され、関数コンポーネントでも状態管理とライフサイクルメソッドが使えるようになりました。

<br><br>
<common-slide/>

---
transition: fade-out
---

# Reactの主な特徴
<br><br>

- コンポーネントベースのアーキテクチャ：Reactは全てのものをコンポーネントと見なし、これらのコンポーネントを組み合わせてユーザーインターフェースを構築します。これはコードの再利用性を高め、可読性を高め、メンテナンスを簡単にします。

- 仮想DOM: Reactは「仮想DOM」という概念を導入し、ブラウザにレンダリングするプロセスを最適化します。これにより、ユーザーインターフェースが効率的に更新されます。

- 一方向のデータフロー: Reactはデータが上から下へ（親から子へ）流れる一方向のデータフローに従います。これは、アプリケーションの状態を簡単に追跡して理解するのに役立ちます。

- JSX: ReactはJavaScript XML(JSX)という文法を使います。JSXはJavaScript内でHTMLを書くことができる文法です。 これにより、開発者はUI構造と動作を一箇所で管理することができます。

<br><br>
<common-slide/>

---
transition: fade-out
---

# React 基本概念 

### jsx
JSXはJavaScript XMLの略で、React要素を生成するJavaScriptの構文拡張です。JavaScript内でHTMLのようなマークアップ文法を使うことができ、UI構造と関連するロジックを一つの空間で処理することができます。
``` 
// html 
<body>
  <script src="script.js"></script> 
</body>
// js
const element = document.createElement("h1");
element.textContent = "Hello, world!";

//jsx
const element = <h1>Hello, world!</h1>;
``` 

<br><br>
<common-slide/>

---
transition: fade-out
---

# Reat 基本概念 

## コンポーネントとProps
- コンポーネント 
  - ReactはUIを独立した再利用可能な小さな部分である「コンポーネント」に分けて管理します。コンポーネントはJavaScript関数やクラスで表現され、React要素を返します。簡単なコンポーネントは下記のようなものです。
<br>

```
// Welcomeというコンポーネントの定義
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>;
}

// コンポーネントの使用 
<Welcome name="React" />;
// H1 タグを使ってHello、Reactを出力します。 
```

<br>
<common-slide/>

---
transition: fade-out
---

# Reat 基本概念 

### コンポーネントとProps
- Props 
  - Propsはコンポーネントに渡されるデータを意味します。コンポーネントの再利用性を高め、データを通じてコンポーネントの動作と出力を制御することができます。
    - Propsのコンポーネントの再利用性についてもう少し具体的に説明すると、同じコンポーネントを別のpropsで複数回使用したり、状況によって違うコンポーネントをレンダリングするなどの作業が可能です。

```
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

```

<br><br>
<common-slide/>

---
transition: fade-out
---
### StateとLifeCycle
- 状態
    - Stateはコンポーネントで管理されるデータを意味します。このデータはコンポーネントがレンダリングされる時に使用され、状態が変更されるとコンポーネントは再レンダリングされます。
    - Stateはコンポーネント内でのみアクセス可能で、**`setState`**メソッドで更新することができます。
    - Stateが変更されると、コンポーネントは再レンダリングされます。
```
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0); 
  return (
    <div>
      <p>You clicked {count} times</p>
       <button onClick={() => setCount(prevCount => prevCount + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;
```

<br><br>
<common-slide/>

---
transition: fade-out
---

### StateとLifeCycle
<br>

- ライフサイクル
  - ライフサイクルはコンポーネントの生成から消滅までの様々な段階を説明します。 各段階ごとに特定のメソッドが呼び出されます。このようなメソッドをライフサイクルメソッドと言います。
    - マウント(Mounting):
      - constructor(): コンポーネントが最初に作成されたときに呼ばれます。
      - render(): コンポーネントのUIを描画します。
      - componentDidMount(): コンポーネントがDOMに追加された後に呼ばれます。データの取得や初期化処理などを行うのに適しています。
    - アップデート(Updating):
      - render(): コンポーネントのUIを再描画します。
      - componentDidUpdate(): コンポーネントが更新された後に呼ばれます。状態やプロパティの変更に対する応答を処理するのに使用されます。
    - アンマウント(Unmounting):
    - componentWillUnmount(): コンポーネントがDOMから削除される前に呼ばれます。リソースの解放やクリーンアップなどの処理に使用されます。
  

<br><br>
<common-slide/>

---
transition: fade-out
---


### StateとLifeCycle
<br>

- ライフサイクル
  - Reactコンポーネントのライフサイクルに関するアプローチが変更されました。クラスコンポーネントの古典的なライフサイクルメソッドに代わるものとして、Hooksが導入されました。Hooksを使用することで、関数コンポーネントでも状態の管理やライフサイクルに関する処理を行うことができるようになりました。
    - useState: 状態を管理するためのフックです。クラスコンポーネントでのthis.stateと同じように状態を管理できます。
    - useEffect: マウント、アップデート、アンマウント時に特定の処理を行うためのフックです。クラスコンポーネントのcomponentDidMount、componentDidUpdate、componentWillUnmountに対応します。
    - useContext: コンテクストを使用するためのフックで、コンテクスト内の値にアクセスすることができます。
    - useReducer: useStateと同様に状態を管理するためのフックですが、より複雑な状態のロジックやアクションの管理に使用されます。
    - useMemo: 計算結果のメモ化を行うためのフックで、コンポーネントが再レンダリングされても計算を最適化します。
    - useCallback: コールバック関数のメモ化を行うためのフックで、コンポーネントの再レンダリング時に不必要な再生成を防ぎます。
    - useRef: 参照を管理するためのフックで、DOM要素へのアクセスや変数の保持に使用されます。

<br><br>
<common-slide/>

---
transition: fade-out
---

### React vs Vue

- 反応性システム：
  - Vue: 宣言的なデータバインディングを使います。 dataオブジェクトの属性が変更されると自動的にビューが更新されます。
  - React: setStateやuseStateフックを使って状態変更を通知してコンポーネントを再レンダリングします。

- テンプレート vs JSX：
  - Vue: HTMLベースのテンプレートを使ってUIを宣言的に定義します。オプションでJSXを使うこともできます。
  - React: JSX (JavaScript XML)を使ってUIを定義します。   
<br>
<common-slide/>

---
transition: fade-out
---

### React vs Vue

- スタイリング：
  - Vue: Single File Componentsで`<style>`タグ内にCSSを含めることができるようになりました。スコープされたCSSやCSSモジュールもサポートされます。
  - React: CSS-in-JS ライブラリ(例えば、styled-components, emotion)を使うか、伝統的なCSSやCSSモジュールを使うことができます。

- API＆デザインパラダイム：
  - Vue: Options APIとVue 3で導入されたComposition APIを提供します。
  - React: 関数型コンポーネントとフックを使います。クラスコンポーネントもサポートされますが、最近は関数型コンポーネントが推奨されます。  

<br>
<common-slide/>
---
transition: fade-out
---

### React vs Vue

- タイプスクリプトをサポート：
  - Vue: Vue 3でTypeScriptのサポートが改善されました。
  - React: TypeScriptとの互換性が高く、多くのコミュニティサポートがあります。

<br>

<common-slide/>

---
transition: fade-out
---

### React vs Vue

- React vs Composition API vs options API

<a href="https://ibb.co/bz92Qw5"><img src="https://i.ibb.co/jgXWb0k/1.png" alt="1" ></a>
<br>
<common-slide/>

---
transition: fade-out
---

# ありがとうございます