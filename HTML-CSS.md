# ちらしやドットコム スタイルガイド

## 目的
- コードの品質のばらつきを減らす。
- コードディングでの迷いを減らす

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

### ローカルルールも尊重する
- コードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務める。もし一貫したルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く方が良い。

## HTML/CSS共通ルール
### 目的に応じたマークアップ(セマンティックなマークアップ)をする
HTML要素は目的に応じて使う。例えば見出しはh1～h6要素、段落にはp要素を使う、など。
適切な場所でsection、article、figure、dl要素なども使う。

### 構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする
コードを見て論理構造がわかるようにインデントをつける。<br>
テキストエディタのデフォルトの設定ではインデントがスペース４つになっていることが多いが、  
ネストが深くなると読みにくくなるため、インデントはスペース２つに設定する。<br>
タブはインデントに使用しない。

```html
<!--【OK】スペース2つでインデントがつけられている -->
<dl class="form-item">
  <dt class="form-item__title">名前</dt>
  <dd class="form-item__desc">
　  <input class="form-item__input text-field" type="text" name="name">
  </dd>
</dl>
```
```html
<!-- 【NG】インデントが適切に設定されていない -->
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
HTMLで最も一般的な記法
```html
<!--【OK】ハイフンつなぎ(ケバブケース) -->
<h1 class="top-level-heading">ちらし屋ドットコム</h1>
```
```html
<!--【一応OK】大文字つなぎ(キャメルケース)
こちらもNGではないが、原則ケバブケースを優先する。 -->
<h1 class="topLevelHeading">ちらし屋ドットコム</h1>
```
#### ▽例【NG】アンダースコアつなぎ(スネークケース)
我流コーダーこの記法を好む人は少なくないが、HTMLでこの記法に用いるのは推奨しない。<br>
(PHPやRubyの変数名の命名にはよく使われる）
```html
<h1 class="top_level_heading">ちらし屋ドットコム</h1>
```

### クラス名やid名はできるだけ一般的な名前をつけ、名前の短さよりもわかりやすさを優先する
```html
<!-- 【OK】長くてもわかりやすさ優先 -->
<button class="hamburger-button" id="hamburger-button"></button>
```
```html
<!-- 【OK】略語でもすぐに意味がわかるものはOK -->
<button class="ham-button" id="ham-button"></button>
```
```html
<!-- 【NG】hbが何を意味するのかわかりづらい -->
<button class="hb" id="hb"></button>
```

### ローマ字での命名はしない

OK `heading image`<br>
NG `midashi gazou`

### img要素にはalt属性を必ずつける
```html
<!--【OK】-->
<img src="./images/sample.png" alt="サンプル画像">
<!--【OK】説明が不要ならばalt属性は空欄でもよい（alt属性自体の省略は認められない） -->
<img src="./images/foo.png" alt="">
```
### a要素にtarget="_blank"属性を付ける場合は、rel="noopener noreferrer"属性もつける
XSS攻撃に対する脆弱性を防ぐため。
```html
<!--【OK】-->
<a href="/newpage.html" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
<!--【NG】-->
<a href="/newpage.html" target="_blank">新しいタブで開く</a>

```
### 画像ファイルの命名
役割がわかるように接頭辞をいれることを推奨する<br>
接頭辞の例
- ico_ アイコン（例 ico_star.png）
- pic_ 写真
- txt_ テキスト
- bg_ 　背景
- arrow_ 矢印
など

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

#### ▽コメントの例
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

谷拓樹氏の書籍「Web制作者のためのCSS設計の教科書」によると、良いCSSは
- 予測しやすい
- 保守しやすい
- 最利用しやすい
- 拡張しやすい
という特徴がある。このCSSスタイルガイドもこの４点を満たすCSSを書くことを目指す。

### 不要なスタイルの重複がある 
不要な重複記述は保守性を悪化させるため、不必要なスタイルの記述の重複がないようする。

```css
/*【NG】無駄な重複がある。 */
.text {
  color: #333;
  font-size: 24px;
  line-height: 1.6;
  letter-spacing: 0.01em;
  margin-bottom: 20px;
}
@media screen and (max-width: 900px) {
  .text {
    color: #333; /* ※重複 */
    font-size: 20px; 
    line-height: 1.6; /* ※重複 */
    letter-spacing: 0.01em; /* ※重複 */
    margin-bottom: 14px; 
  }
}
/* 【OK】不要な重複がない */ 
.text {
  color: #333;
  font-size: 24px;
  line-height: 1.6
  letter-spacing: 0.01em;
  margin-bottom: 20px;
}
@media screen and (max-width: 900px) {
  .text {
    font-size: 20px;
    margin-bottom: 14px; 
  }
}
```

### スタイルを当てる際は原則クラスセレクタを利用する。
スタイルをクラスに当てることは以下のようなメリットがある。<bt>
(idセレクタや要素セレクタにスタイルを当てることのデメリットについては後述する。)
- スタイルの影響範囲を限定できる
- スタイルの再利用がしやすい
- スタイルの詳細度をある程度一定に保つことができるので、上書きや変更がしやすい。

```css
/* 【OK】クラスセレクタにスタイルを当てている */
.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### セレクタのネストは最小限にする
セレクタのネストは便利な一方で以下のようなデメリットがあるので、できるだけネストは最小限にする。<br>
- ネストをするとスタイルが特定のコンテキストに依存させることになるため、再利用がしにくくなる。
- ネストはスタイルの詳細度を高めるため、乱用するとスタイルのあとから上書きがしにくくなる。

```css
/* 【NG】不要なネストがある
以下のような記述だと、".top-level-heading"用のスタイルは.headerの中でしか効かないため、.header外の場所で再利用できない。 */
.header .top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
### 要素セレクタを併記しない
スタイルが要素名に依存してしまうのでNG。<br>
例えば、HTML側でh1をpに変更した場合、スタイルが効かなくなってしまうので、メンテナンス性が悪い。

```css
/* 【NG】要素セレクタを併記している */
h1.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### 要素セレクタ単体にスタイルを当てない
要素セレクタ単体にスタイルを当てると、影響範囲が広すぎるため意図しないところでのスタイルが崩れる可能性がある。<br>
要素セレクタ単体にスタイルを当てるのは、スタイルをリセットするときのみにする。

```css
/* 【NG】スタイルを要素セレクタに直接設定している */
h1 {
  padding: 10px 0;
  font-size: 20px;
  color: #333;
  letter-spacing: 0.04em;
  text-align: center;
}
```
#### ▽例【OK】要素セレクタにリセット用のスタイルを設定するのはOK
```css
/* 【OK】スタイルのリセット */
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
- idセレクタはスタイルの詳細度を不必要に高めてしまうのであとから調整がききにくくなる。
- 同じidは1ページにつき１つという決まりがあるためスタイルの再利用がしにくくなる
idはページ内リンクやJavaScriptでのDOM操作のみに使用する。

```css
/* 【NG】idにスタイルを当てている */
#top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
```css
/* 【NG】idをセレクタに使用している */
#main h1 {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### Utilityクラスの濫用は避ける
Utilityクラスとは、特定の一つのCSSプロパティだけが割り当てられたクラスのこと。<br>
Utilityクラスは部分的に使うと便利な時があるが、乱用すると細かい調整が必要になった時に修正がしづらいので多様しないことを推奨する。

#### ▽NG 
```html
<div class="mb50 bold bg-gray p10">
　Hello, world!
<div>
```
```css
.mb50 { margin-bottom: 50px; }
.p10 { padding: 10px; }
.bold { font-weight: bold; }
.bg-gray { background-color: #ddd; }
```
#### ▽OK
```html
<div class="message-box">
　Hello, world!
<div>
```
```css
.message-box {
  backgorund-color: #ddd;
  font-weight: bold;
  margin-bottom: 50px;
  padding: 10px;
}
```
### インラインスタイルは原則使用しない
スタイルの記述場所が分散するため、インラインスタイルは原則使用しない。<br>
ただし、状況によってはbackground-imageなどはインラインスタイルで使用しても良い。
#### ▽NG
```html
<div class="message-box" style="color: red">
　Hello, world!
<div>
```
```css
.message-box {
  backgorund-color: #ddd;
  font-weight: bold;
  margin-bottom: 50px;
  padding: 10px;
}
```
#### ▽OK (BEMのModifier(後述)を使用している)
```html
<div class="message-box message-box--color_red">
　Hello, world!
<div>
```
```css
.message-box {
  background-color: #ddd;
  font-weight: bold;
  margin-bottom: 50px;
  padding: 10px;
}
.message-box--color_red {
  color: red;
}
```

### その他
#### 単位の指定について
- font-size 
基本的に固定値(px, remなど)で設定する。
スマホ・タブレット用のコーディングで普通の段落文字のfont-sizeをvwで指定するのは避ける。画面幅によって文字の大きさが極端に大きくなることを避けるため。
ただし、見出しなどの一部の要素でデザインの都合上vwを使ったほうが良さそうな場合はvwでもOK）

- line-height
単位なしの相対値で設定する。pxなどの固定値で設定しない。

- letter-spacing
単位はemで設定する。

#### Sassについて
可能であれば、CSSプリプロセッサのSassを使用する。<br>
Sassを導入することで、スタイルを書くときの効率や保守性が上がる。<br>
Sassを使う際は、拡張子が.scssのSCSS記法で書く。

#### レスポンシブ対応について
##### ブレイクポイント
PC用、タブレット用、スマホ用の３種類のデバイスに対応するようにスタイルを組む。ブレイクポイントはデザイン応じて適したものを選ぶ。 <br>
以前主流だったブレイクポイントが786pxの一点のみという設計は時代遅れになりつつあるので推奨しない。

##### メディアクエリはモジュール単位で記述する。
media queryをブレイクごとにすべてまとめて記述する方法は表示速度の点ではやや有利だが、
メンテナンス性が良くないのでモジュールごとに記述すること推奨する。<br>
Sassを使用している場合は要素ごとにミックスインでメディアクエリ用のスタイルを設定する。
```css
/* CSSの場合 モジュールごとにメディアクエリを指定　*/
.top-level-heading {
  padding: 10px 0;
  font-size: 38px;
  letter-spacing: 0.04em;
  text-align: center;
}

@media screen and (max-width: 940px){
  .top-level-heading {
    padding: 5px 0;
    font-size: 27px
  }
}

@media screen and (max-width: 600px){
  .top-level-heading {
    font-size: 22px
  }
}

.data-list {
  background-color: #ddd;
  margin-bottom: 50px;
  padding: 10px;
}
.data-list__title {
  font-weight: bold;
  font-size: 24px;
}

@media screen and (max-width: 940px){
  .data-list {
    padding: 5px;
  }
  .data-list__title {
    font-size: 20px;
  }
}

@media screen and (max-width: 600px){
  .data-list__title {
    font-size: 16px;
  }
}

```
```scss
// Sass(SCSS記法)の場合

//事前にミックスインを定義
@mixin tab {
  @media screen and (max-width: 940px){
    @content;
  }
}

@mixin sp {
  @media screen and (max-width: 600px){
    @content;
  }
}

//要素ごとにミックスインをインクルードする
.top-level-heading {
  padding: 10px 0;
  font-size: 24px;
  letter-spacing: 0.04em;
  text-align: center;
  @include tab {
    padding: 5px 0;
    font-size: 38px;
  }
  @include sp {
    font-size: 22px;
  }
}

.data-list {
  background-color: #ddd;
  margin-bottom: 50px;
  padding: 10px;
  @include tab {
    padding: 5px;
  }
  &__title {
    font-weight: bold;
    font-size: 24px;
    @include tab {
      font-size: 20px;
    }
    @include sp {
      font-size: 16px;
    }
  }
}

```

## CSSの書き方（実践編）
執筆中