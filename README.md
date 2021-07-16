# ちらしやドットコム スタイルガイド

## 目的
コードの品質のばらつきを減らす。<br>
修正・保守がしやすいコードを書くことは、中長期的には業務の効率化につながる。

## はじめに
HTML/CSSはコーディングの自由度が高いが、コーダーが独自のルールで運用するとルールや設計が破綻しやすいので、品質を維持するためには一定のルールセットの導入が必要である。<br>
本コーディングガイドは以下のドキュメントや書籍を参考に作成している。

### 基本的なコーディングスタイル
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)

### CSS設計手法
- [Methodology BEM(BEM公式ドキュメント)](https://en.bem.info/methodology/quick-start/)
- [CSS設計完全ガイド(書籍)](https://gihyo.jp/book/2020/978-4-297-11173-1)

## 基本原則
### メンテナンス性の高いコードを書く。
- 一度書いたら終わりではなく、継続的に保守されることを前提にコードを書く。
- 自分以外の第三者が見ても理解しやすいコードを書くように務める。

### ローカルルールを尊重する
- コードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務め、一貫したローカルルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く。

## HTML/CSS共通ルール

### 構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする
コードを見て論理構造がわかるようにインデントをつける。<br>
テキストエディタのデフォルトの設定ではインデントがスペース４つになっていることが多いが、  
ネストが深くなると読みにくくなるため、インデントはスペース２つに設定する。
タブはインデントに使用しない。

```html
<!--OK(スペース2つでインデントがつけられている) -->
<dl class="form-item">
  <dt class="form-item__title">名前</dt>
  <dd class="form-item__desc">
　  <input class="form-item__input text-field" type="text" name="name">
  </dd>
</dl>

<!--NG(インデントが適切に設定されていない)-->
<dl class="form-item">
<dt class="form-item__title">名前</dt>
<dd class="form-item__desc">
<input class="form-item__input text-field" type="text" name="name">
</dd>
</dl>
```
```css
/* OK(スペース2つでインデントがつけられている) */
@meida screen and (max-width: 900px) {
  .logo {
    font-size: 24px;
  }
}

/* NG(インデントが適切に設定されていない) */ 
@meida screen and (max-width: 900px) {
.logo {
  font-size: 24px;
}
}
```
### 単語の区切りには-(ハイフン)を使う
id名やクラス名に複数単語からなる語を当てる場合、記法単語の区切りは原則ハイフンは用いる。
#### 【OK】ハイフンつなぎ(ケバブケース)
HTMLで最も一般的な命名法
```html
<h1 class="top-level-heading">ちらし屋ドットコム</h1>
```
#### 【一応OK】大文字つなぎ(キャメルケース)
こちらもNGではないが、原則ケバブケースを優先する。
```html
<h1 class="topLevelHeading">ちらし屋ドットコム</h1>
```
#### 【NG】アンダースコアつなぎ(スネークケース)
HTMLでこの命名法に用いるのは推奨しない。
```html
<h1 class="top_level_heading">ちらし屋ドットコム</h1>
```

### クラス名やid名はできるだけ一般的な名前をつけ、名前の短さよりもわかりやすさを優先する
#### 【OK】長くてもわかりやすさ優先
```html
<button class="hamburger-button" id="hamburger-button"></button>
```
#### 【OK】略語でもすぐに意味がわかるものはOK
```html
<button class="ham-button" id="ham-button"></button>
```
#### 【NG】hbが何を意味するのかわかりづらい
```html
<button class="hb" id="hb"></button>
```

### ローマ字での命名はしない

OK `heading image`<br>
NG `midashi gazou`

## CSSのスタイルガイド
### CSSの基本フォーマット
以下のフォーマットに従って書く。
```css
.selector { 　　/* セレクター名(.selector)と{の間はスペースを一つ空ける */
  font-size: 16px;  /* プロパティ名(font-size)の後ろのコロン(:)と値(16px)の間はスペース１つ空ける */
  letter-spacing: 0.1em;
}   /* 閉じカッコは新しい行に入れる */
   /* 新たなセレクタを書くときは１行空ける */
.selector-foo,  /* 複数セレクタを指定する場合は改行をする */
.selector-bar,
.selector-baz {　
  margin: 0; 
  padding: 0;
}
```

### 適宜コメントを入れる
スタイルが何のためのものなのかわかるようにCSSファイルに適宜コメントを書くようにする。

#### コメントの例
```css
/* スタイルのリセット */
img {
  vertical-align: left;
  max-width: 100%;
}

/* レイアウト用 */
.inner {
 width: 960px;
 margin: 0 auto;
}
```
## CSSの書き方（基本編）

谷氏によると良いCSSは
- 予測しやすい
- 保守しやすい
- 最利用しやすい
- 拡張しやすい
という特徴がある。このCSSスタイルガイドは、この４点を満たすCSSを書くことを目指すものである。

### スタイルを当てる際は原則クラスセレクタを利用する。
スタイルをクラスに当てることは以下のようなメリットがある。<bt>
(idセレクタや要素セレクタにスタイルを当てることのデメリットについては後述する。)
- スタイルの再利用がしやすくなる。
- スタイルの影響範囲を特定しやすい。
- スタイルの詳細度をある程度一定に保つことができるので、上書きや変更がしやすい。

#### 【OK】クラスセレクタにスタイルを当てている
```css
.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### 不必要な親セレクタのネストはしない。
以下のような理由から、不要なネストは避ける。
- ネストをするとスタイルが特定のコンテキストに依存させることになるため、再利用がしにくくなる。
- ネストはスタイルの詳細度を高めるため、乱用するとスタイルのあとから上書きがしにくくなる。

### 例
以下のような記述だと、".top-level-heading"用のスタイルは.headerの中でしか効かないため、.header外の場所で再利用できない。
```css
.header .top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
### 要素セレクタを併記しない
スタイルが要素名に依存してしまうのでNG。<br>
例えば、HTML側でh1をpに変更した場合、スタイルが効かなくなってしまう

```css
h1.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### 要素セレクタ単体にスタイルを当てない
要素セレクタ単体にスタイルを当てると、影響範囲が広すぎるため意図しないところでのスタイルの崩れる可能性がある。<br>
要素セレクタ単体にスタイルを当てるのは、スタイルをリセットするときのみにする。

#### 【NG】スタイルを要素セレクタに設定している
```css
h1 {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
#### 【OK】要素セレクタにリセット用のスタイルを設定するのはOK
```css
/* スタイルのリセット */
img {
  vertical-align: top;
  max-width: 100%;
}
ul {
  list-style-type: none;
}
```

### スタイルにidセレクタを使用しない
スタイル設定にidセレクタは使用すると以下のようなデメリットがあるので避ける。
・idセレクタはスタイルの詳細度を不必要に高めてしまうのであとから調整がききにくくなる。
・同じidは1ページにつき１つという決まりがあるためスタイルの再利用がしにくくなる
idはページ内リンクやJavaScriptでのDOM操作のみに使用する。

#### NG
```css
#top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
#### これもNG
```css
#main h1 {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```