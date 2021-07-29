# ちらしやドットコム HTML/CSS スタイルガイド(基本編)

## はじめに
HTML/CSSのコーディングは自由度が高いため、コーダーが独自のルールで書くと修正や拡張がしにくいコードが作られがちです。<br>
そのような事態を回避するには、一貫した規則や設計のもとにコードを書くことが重要です。<br>
一貫したルールや設計のもとでコードを書くことにより以下のような効果が期待できます。<br>
- コードの品質を一定以上にたもつことができる
- 保守や修正にかかる労力を削減することができます。
- コードを書く際の迷いが減るため開発スピードが向上します。<br>

本ドキュメントでは、メンテナンス性が高いコードを書くために重要だと思われるポイントをスタイルガイドとしてまとめました。<br>
なお、本スタイルガイドは以下のドキュメントや記事を参考に作成しています。
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [こんなHTMLとCSSのコーディング規約で書きたい](https://qiita.com/pugiemonn/items/964203782e1fcb3d02c3)

## 基本方針
### メンテナンス性の高いコードを書く。
- 一度書いたら終わりではなく、継続的に保守されることを前提にコードを書く。
- 自分以外の第三者が見ても理解できるコードを書くこと意識する。

### ローカルルールも尊重する
- コードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務める。もし一貫したルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く方が良い。

## HTML/CSS基本ルール

### 目的に応じたマークアップ(セマンティックなマークアップ)をする
HTML要素は目的に応じたものを選んで使う。例えば見出しはh1～h6要素、段落にはp要素を使う、など。

### 構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする
コードを見て論理構造がわかるようにインデントをつける。<br>
テキストエディタのデフォルトの設定ではインデントがスペース４つになっていることが多いが、  
ネストが深くなると読みにくくなるため、インデントはスペース２つを推奨する。<br>
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
```css
/* OK(スペース2つでインデントがつけられている) */
@meida screen and (max-width: 900px) {
  .logo {
    font-size: 24px;
  }
}
```
### 単語の区切りには-(ハイフン)を使う
id名やクラス名に複数単語からなる語を当てる場合、記法単語の区切りは原則ハイフンを用いる。

```html
<!--【OK】ハイフンつなぎ(ケバブケース) 
HTMLで最も一般的な記法　-->
<h1 class="top-level-heading">ちらし屋ドットコム</h1>
```
```html
<!--【一応OK】大文字つなぎ(キャメルケース)
こちらもNGではないが、原則ケバブケースを優先する。 -->
<h1 class="topLevelHeading">ちらし屋ドットコム</h1>
```
```html
<!--　【NG】アンダースコアつなぎ(スネークケース)
PHPやRubyの変数名などの命名にはよく使われる記法だが、HTMLでこの記法を用いるのは推奨しない。 -->
<h1 class="top_level_heading">ちらし屋ドットコム</h1>
```

### クラス名やid名は目的に応じたわかりやすい名前をつける
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
```html
<!-- 【NG】なんのためのボタンかわからない -->
<button class="button1" id="button1"></button>
```

### ローマ字での命名はしない

OK `heading image`<br>
NG `midashi gazou`

### img要素にはalt属性を必ずつける
```html
<!--【OK】-->
<img src="./images/sample.png" alt="サンプル画像">
```
```html
<!--【OK】画像への説明が不要ならばalt属性は空欄でもよい（alt属性自体の省略は認められない） -->
<img src="./images/foo.png" alt="">
```
### a要素にtarget="_blank"属性を付ける場合は、rel="noopener noreferrer"属性もつける
XSS攻撃に対する脆弱性を防ぐため。
```html
<!--【OK】-->
<a href="/newpage.html" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
```
```html
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

### HTMLを一通り書いてからCSSを書く
HTMLとCSSは同時に書くのは避ける。HTMLとCSSを並行して書くと、設計にブレが生じやすく、コーディングスピードも遅くなる。<br>
HTMLを書き終わってからCSSを書くほうが、設計に一貫性をもたせやすく、コーディング完了までのスピードも速くなる。

## CSSのスタイルガイド（基礎編）

谷拓樹氏の書籍「Web制作者のためのCSS設計の教科書」によると、良いCSSは
- 予測しやすい
- 保守しやすい
- 最利用しやすい
- 拡張しやすい<br>

という特徴がある。このCSSスタイルガイドもこの４点を満たすCSSを書くことを目指す。

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

### 不要なスタイルの重複記述を避ける
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
```
```css
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

### スタイルは原則クラスに当てる
スタイルは原則としてクラスに記述する。
スタイルをクラスに当てることは以下のようなメリットがある。<br>
- スタイルの影響範囲を限定できる
- スタイルの再利用がしやすい
- スタイルの詳細度をある程度一定に保つことができるので、上書きや変更がしやすい。<br>
idセレクタや要素セレクタにスタイルを当てることのデメリットについては後述する。

```css
/* 【OK】クラスセレクタにスタイルを当てている */
.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```
### クラスの命名には一貫した命名規則を採用する(BEMを推奨)
メンテナンス性の高いCSSを書くには、クラスの命名に一貫したルールをもたせるのが非常に重要である。<br>
クラスの命名規則としては、BEMと呼ばれる命名規則を使用することを推奨する。BEMについての解説は後述する。

### 要素セレクタを併記しない
スタイルが要素名に依存してしまうのでNG。<br>
例えば以下の例だと、HTML側でh1をpに変更した場合、スタイルが効かなくなってしまうので、メンテナンス性が悪い。

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

### idセレクタにスタイルを当てない
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
/* 【NG】idセレクタ経由でスタイルを当てている */
#main h1 {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### セレクタのネスト（入れ子）はほどほどに
セレクタを過剰にネストするとスタイルの影響範囲がわかりづらくなったり、コードの可読性が悪くなったりするため、
メンテナンスがしにくいCSSになってしまう。それに加えて、ネストが深いCSSはCSSの読み込み速度を低下させるデメリットもある。<br>
以上の理由から、セレクタのネストが深くなりすぎないように注意することが望ましい。具体的には、ネストをする際は以下のように孫セレクタまでに留めることを推奨する。
```css
親 > 子　> 孫
```
そもそもBEMやSMACSSなどのルールに基づいてクラスを命名していれば、ネストはあまり使う必要がなくなる。

### 原則モジュールごとにスタイルをつける。Utilityクラス中心のスタイリングは非推奨
Utilityクラスとは、特定の一つのCSSプロパティだけが割り当てられたクラスのこと。(Helperクラスと言う場合もある。)<br>
Utilityクラスは部分的に使うと便利な時があるが、乱用すると細かい調整が必要になった時に修正がしづらいので多様しないことを推奨する。

#### ▽NG Utilityクラスを多用してスタイリングしている
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
#### ▽OK モジュールごとにスタイリングしている
```html
<div class="message-box">
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


### 単位に関する注意事項
#### font-size 
基本的に固定値(px, remなど)で設定する。<br>
スマホ・タブレット用のコーディングで普通の段落文字のfont-sizeをvwで指定するのは避ける。画面幅によって文字の大きさが極端に大きくなることを避けるため。<br>
ただし、見出しなどの一部の要素でデザインの都合上vwを使ったほうが良さそうな場合はvwを使用してもよい。

#### line-height
単位なしの相対値で設定する。pxなどの固定値で設定しない。
OK `line-height: 1.6;`<br>
NG `line-height: 20px;`

#### letter-spacing
単位はemで設定する。

### リセットCSSの使用を推奨する
新規のコーディングプロジェクトには原則リセットCSSを使用するほうが良い。<br>
おすすめのリセットCSS
- [destyle.css](https://github.com/nicolas-cusan/destyle.css/blob/master/destyle.css)
- [HTML5 Doctor](http://html5doctor.com/html-5-reset-stylesheet/)

### Sassの使用を推奨する
可能であれば、CSSプリプロセッサのSassを使用を推奨する。<br>
Sassを導入することで、スタイルを書くときの効率や保守性が上がる。<br>
Sassを使う際は、拡張子が.scssのSCSS記法で書く。

### レスポンシブ対応について
#### ブレイクポイント
PC用、タブレット用、スマホ用の３種類のデバイスに対応できるようにスタイルを組む。ブレイクポイントはデザイン応じて適したものを選ぶ。 <br>
以前主流だったブレイクポイントが786pxの一点のみという設計は時代遅れになりつつあるので推奨しない。<br>

#### メディアクエリはモジュール単位で記述する。
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

## CSSのスタイルガイド【実践編：BEM記法でCSSを書く】

CSSは記述の自由度が高いため、一定のルールに基づいて運用しないと簡単にカオス化してしまいます。(“CSS is fragile.” （CSSは壊れやすい）という格言(?)が存在する。)<br>
この問題は、特定のCSS設計手法を導入することによって解決できます。CSS設計手法とは、CSSの書き方に対して、一連の規則を定めたものです。<br>
CSS設計手法の代表的なものには、OOCSS(オーオーシーエスエス)、SMACSS(スマックス)、BEM(ベム)と呼ばれるものがあります。<br>
本スタイルガイドでは、BEMを推奨の設計手法とします。<br>

### BEMとは？
BEMはスタイルを<strong>Block(ブロック)</strong>、<strong>Element(エレメント)</strong>、<strong>Modifier(モディファイア)</strong>の３種類のコンポーネントに分けて設計するCSSの設計手法。
それぞれの頭文字をとってBEMと呼ばれている<br>
- Block<br>
再利用可能な独立したパーツとして定義するもの
- Element<br>
Blockの構成要素として定義するもの。親となるブロックの内部でのみ用いる。
- Modifier<br>
BlockやElementのバリエーションとして定義するもの。見た目、状態、ふるまいなどのバージョン違いを定義する。
block

## BEMの優れている点
- ルールがシンプルかつ厳格なため、堅牢性が高いCSSを書きやすい。
- クラス名を見るだけでコンポーネントの依存関係を瞬時に把握できる
- 慣れればCSSの書き方に迷うことが少なくなるので、開発スピードが上がる。
- Modifierを使うことで既存のスタイルを容易に拡張できる。
- 広く普及している設計手法なので一度覚えたら様々な場所で使うことができる。

## BEMを学ぶ
まずは以下の記事でBEMの基本を理解するのがおすすめです。<br>
- [5分で理解するBEM](https://zenn.dev/knts0/articles/quick-understanding-bem)
- [【CSS設計】今さら聞けないBEMの基本【初心者・入門】](https://nycreation.jp/blog/archives/289)
- [BEMによるCSS設計の方法を解説。命名規則から使い方まで。]https://original-game.com/css-bem/

また、余力があれば以下を学ぶと理解が深まります。<br>
- [Quick Start / Methodology BEM](https://en.bem.info/methodology/quick-start/)<br>
  BEMの公式ドキュメントです。Quick Startのページだけでも目を通す価値はあると思います。(英語が苦手な方はGoogle翻訳を推奨)
- [CSS設計完全ガイド(書籍)](https://gihyo.jp/book/2020/978-4-297-11173-1)<br>
  CSS設計のバイブル的な本です。BEMについて様々な例を上げてかなり詳しく解説されています。
  
## BEM記法のバリエーション--MindBEMdingで書こう

オリジナルのBEM記法では、BlockまたはElementとModifierの区切りをアンダースコア一つでつなぐが、これは少々読みにくいので、代わりにBlockまたはElementとModifierの区切りをハイフン2つでつなげる書き方が考案された。<br>ハイフン２つを用いる記法はMindBEMding記法と呼ばれる。MindBEMding記法の方で書くほうが読みやすいので、MindBEMding記法を採用することを推奨する。

オリジナルの記法の例 `search-form__button_size_s`<br>
MindBEMding記法の例(推奨) `search-form__button--size_s`

