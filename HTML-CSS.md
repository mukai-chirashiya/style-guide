# ちらしや HTML/CSS スタイルガイド


<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=2 orderedList=false} -->

<!-- code_chunk_output -->

- [1. はじめに](#1-はじめに)
- [2. 基本方針](#2-基本方針)
- [3. HTML/CSS基本ルール](#3-htmlcss基本ルール)
- [4. CSSのスタイルガイド](#4-cssのスタイルガイド)
- [5. BEM(CSS設計手法)を導入する](#5-bemcss設計手法を導入する)

<!-- /code_chunk_output -->


## 1. はじめに
HTML/CSSのコーディングは自由度が高いため、コーダーが独自のルールで書くと修正や拡張がしにくいコードが作られがちです。<br>
そのような事態を回避するには、一貫した規則や設計のもとにコードを書くことが重要です。<br>
一貫したルールや設計のもとでコードを書くことにより以下のような効果が期待できます。<br>
- コードの品質を一定以上にたもつことができる
- 保守や修正にかかる労力を削減することができる。
- コードを書く際の迷いが減るため開発スピードが向上する。<br>

本ドキュメントでは、メンテナンス性が高いコードを書くために重要だと思われるポイントをスタイルガイドとしてまとめました。<br>
なお、本スタイルガイドは以下のドキュメントや記事を参考に作成しています。
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [こんなHTMLとCSSのコーディング規約で書きたい](https://qiita.com/pugiemonn/items/964203782e1fcb3d02c3)

## 2. 基本方針
### メンテナンス性の高いコードを書く。
- 一度書いたら終わりではなく、継続的に保守されることを前提にコードを書く。
- 自分以外の第三者が見ても理解できるコードを書くこと意識する。

### ローカルルールも尊重する
- もし既存のコードに修正や追加をする場合は、まずコードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務める。<br>
  もし一貫したルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く方が良い。

## 3. HTML/CSS基本ルール

### 目的に応じたマークアップ(セマンティックなマークアップ)をする
HTML要素は目的に応じたものを選んで使う。例えば見出しはh1～h6要素、段落にはp要素を使う、など。

### 構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする
コードを見て論理構造がわかるようにインデントをつける。<br>
テキストエディタのデフォルトの設定ではインデントがスペース４つになっていることが多いが、  
ネストが深くなると読みにくくなるため、インデントはスペース２つを推奨する。<br>
タブはインデントに使用しない。<br>
※Visual Studio Codeなどのテキストエディタではネストの種類(スペースorタブ)や大きさ(何個分)か変更できる。<br>
ネストの種類にスペースが設定されている場合は、TABキーを押してもネストした部分にはテキストエディタによってスペースが入力されている。

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

### クラス名やID名の命名について
#### 単語の区切りには-(ハイフン)を使う
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

#### 目的に応じたわかりやすい名前をつける
ハンバーガーボタンのクラスのネーミング例
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
<!-- 【NG】button1がハンバーガーボタンだとわからない -->
<button class="button1" id="button1"></button>
```
#### ローマ字での命名はしない

OK `heading image`<br>
NG `midashi gazou`


### 画像の取り扱いについて

- 画像を使わずともCSSで再現できそうなものはできるだけCSSで再現するようにする。一般的にはCSSのほうがきれいに表示され、読み込み速度も速い。
- 文字は原則として画像を利用すべきではなく、HTMLのテキストとして打ち込むべきである。<br>
  ただし、デザインで指定されているフォントが有料フォントの場合で、テキストの内容が変更される可能性が低い箇所については、<br>
  テキストを画像として配置しても良い。その場合、以下の点に注意する。
  - ファイル形式はPNGよりSVG形式が望ましい
  - alt属性にテキストの内容を必ず打ち込む

- 画像のサイズ・形式について
  - 写真はJEPG形式を用いる。ファイルサイズが大きい場合は圧縮する。大きめの画像でも200MB以下になるのが望ましい。
  - アイコンやテキスト画像は、SVG形式で書き出せる場合はSVG形式を使うのが望ましい。SVGで書き出せない場合はPNG形式を利用する。
  - ビットマップ形式で画像を書き出す場合に、高解像度ディスプレイに対応するためにできれば2xの解像度で書き出すのが望ましい。

#### img要素にはalt属性を必ずつける
```html
<!--【OK】-->
<img src="./images/sample.png" alt="サンプル画像">
```
```html
<!--【OK】画像に関する説明が不要であれば、alt属性の値は空でもOK(※alt属性自体の省略はNG) -->
<img src="./images/foo.png" alt="">
```

#### img要素に必要に応じてwidth属性とheight属性を記述する
ページの読み込み速度に有利と言われている。<br>
また、SVG形式の画像や、2xの解像度で書き出した画像のデフォルトの大きさを設定するのに使うと便利。
```html
<!--【OK】width、heightの片方だけでも良い -->
<img src="./images/sample.png" alt="サンプル画像" width="120">
```
```html
<!--【OK】必須というわけではない -->
<img src="./images/sample.png" alt="サンプル画像">
```

#### 画像ファイルの命名
役割がわかるように接頭辞をいれることを推奨する<br>

接頭辞の例
- ico_ アイコン（例 ico_star.png）
- pic_ 写真
- txt_ テキスト
- bg_ 　背景
- arw_ 矢印<br>
など

### a要素にtarget="_blank"属性を付ける場合は、rel="noopener noreferrer"属性もつける
XSS攻撃に対する脆弱性を防ぐため。
```html
<!--【OK】-->
<a href="https://www.example.com/" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
```
```html
<!--【NG】-->
<a href="https://www.example.com/" target="_blank">新しいタブで開く</a>

```

### HTMLを一通り書いてからCSSを書く
HTMLとCSSは同時に書くのは避ける。HTMLとCSSを並行して書くと、設計にブレが生じやすく、コーディングスピードも遅くなる。<br>
HTMLを書き終わってからCSSを書くほうが、設計に一貫性をもたせやすく、コーディング完了までのスピードも速くなる。

## 4. CSSのスタイルガイド

GoogleのエンジニアPhilip Waltonによる記事「[CSS Architecture](https://philipwalton.com/articles/css-architecture/)」では、CSSを設計する時に目指すべき４つのゴールが紹介されている。
- 予測しやすい - クラス名や構造などからふるまいを容易に想像できる。
- 再利用しやすい - 必要に応じて他の場所でも同じように使いまわしができる。
- 保守しやすい - 新たな要素を追加したり、既存の要素を修正したりしたりした時に、他の要素を壊すことがない。
- 拡張しやすい - 誰かがCSSを後に編集することになっても、容易に編集できる。<br>

このCSSスタイルガイドもこれらのゴールを満たすCSSを書くことを目指している。

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

- コメントの例
```css
/* スタイルのリセット */
img {
  vertical-align: top;
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
  margin-bottom: 20px;
  color: #333;
  font-size: 24px;
  line-height: 1.6;
  letter-spacing: 0.01em;
}
@media screen and (max-width: 900px) {
  .text {
    margin-bottom: 14px; 
    color: #333; /* ※重複 */
    font-size: 20px; 
    line-height: 1.6; /* ※重複 */
    letter-spacing: 0.01em; /* ※重複 */
  }
}
```
```css
/* 【OK】不要な重複がない */ 
.text {
  color: #333;
  font-size: 24px;
  line-height: 1.6;
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
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
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
- ▽要素セレクタにリセット用のスタイルを設定するのはOK
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
- 同じidは1ページにつき１つという決まりがあるためスタイルの再利用がしにくくなる。<br>

idはページ内リンクやJavaScriptでのDOM操作のみに使用する。

```css
/* 【NG】idにスタイルを当てている */
#top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```
```css
/* 【NG】idセレクタ経由でスタイルを当てている */
#main h1 {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
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

### モジュールごとにスタイルをつける
スタイルは原則としてモジュールごとに定義する。Utilityクラス中心のスタイリングは推奨しない。<br>
Utilityクラスとは、特定の一つのCSSプロパティだけが割り当てられたクラスのこと。(Helperクラスと言う場合もある。)<br>
Utilityクラスは部分的に使うと便利な時があるが、乱用すると細かい調整が必要になった時に修正がしづらいので多様しないことを推奨する。
- ▽NG Utilityクラスを多用してスタイリングしている
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
- ▽OK モジュールごとにスタイリングしている
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
- ▽NG (インラインスタイルを使用している)
```html
<div class="message-box" style="color: red">
　Hello, world!
<div>
```
```css
.message-box {
  padding: 10px;
  margin-bottom: 50px;
  font-weight: bold;
  background-color: #ddd;
}
```
- ▽OK (BEMのModifier(後述)を使用している)
```html
<div class="message-box message-box--color_red">
　Hello, world!
<div>
```
```css
.message-box {
  padding: 10px;
  margin-bottom: 50px;
  font-weight: bold;
  background-color: #ddd;
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
```css
/* 【NG】 font-sizeにvwは原則使わない */
@media screen and (max-width: 540px){
  .plain-text-box {
    font-size: 4vw;
  }
}
```
```css
/* 【OK】 font-sizeを固定値で指定している */
@media screen and (max-width: 540px){
  .plain-text-box {
    font-size: 15px;
  }
}
```
#### line-height
単位なしの相対値で設定する。pxなどの固定値で設定しない。<br>
OK `line-height: 1.6;`<br>
NG `line-height: 20px;`

#### letter-spacing
単位はemで設定する。<br>
OK `letter-spacing: 0.04em`<br>
NG `letter-spacing: 1px`

### リセットCSSを使用する
新規のコーディングプロジェクトには原則リセットCSSを使用するほうが良い。<br>

おすすめのリセットCSS
- [destyle.css](https://github.com/nicolas-cusan/destyle.css/blob/master/destyle.css)
- [HTML5 Doctor](http://html5doctor.com/html-5-reset-stylesheet/)

### Sassでスタイルを書く
新規のプロジェクトでCSSを書く場合は、CSSプリプロセッサのSassを使用する。<br>
Sassを導入することで、スタイルを書くときの効率や保守性が格段に上がる。<br>
Sassを使う際は、拡張子が.scssのSCSS記法で書く。

#### Sassのコンパイル方法
Visual Studio Codeを使用している場合、Live Sass Compilerという拡張機能でSassをコンパイルするのがおすすめ。
- 参考記事： [Visual Studio CodeでSassを自動でコンパイルする](https://blanche-toile.com/web/vscode-live-sass-compiler)

#### Sassでのファイル分割
ファイル分割する場合は、パーシャルを用いてコンパイル後のファイルの数ができるだけ少なくなるようにする。
- ディレクトリ構成例
```
root/
  ├─ css/
  │  └─style.css コンパイル後のファイル
  └─ sass/
     ├─base
     │  ├─_define.scss 変数とmixinとWebFontのimport
     │  ├─_reset.scss リセットCSS 
     │  └─_base.scss 追加のリセットスタイル
     ├─layout
     │  ├─_layout.scss レイアウトに関するblock
     │  ├─_header.scss headerでのみ使われるblock
     │  └─_footer.scss footerでのみ使われるblock
     ├─component
     │  ├─_heading.scss 汎用見出しblock
     │  ├─_button.scss 汎用ボタンblock
     │  └─_component.scss その他汎用block
     ├─page 
     │  ├─_top.scss トップページでのみ使われるblock
     │  ├─_about.scss aboutページでのみ使われるblock
     │  ├─_company.scss companyページでのみ使われるblock
     │  └─_contact.scss contactページでのみ使われるblock
     └─style.scss すべてのSassファイルをimportするファイル
```

#### Sassの書き方に関する注意事項
- メディアクエリはMixinを利用して書く。詳しくは次項を参照。
- BEMでElementやModifireを書く場合は以下のように`&`を用いたクラス名の継承をする
```scss
.data-list {
  padding: 10px;
  margin-bottom: 50px;
  background-color: #ddd;
  &__title {
    margin-bottom: 8px;
    font-weight: bold;
    font-size: 24px;
    &--color_danger {
      color: red;
    }
  }
  &__desc {
    font-size: 15px;
  }
}

```
- Extendは使用しない
```scss
// 【NG】
.button {
  padding: 8px;
  width: 300px;
  border-radius: 100%;
  background-color: #333;
  color: white;
  text-align: center;
  font-size: 16px;
}
.small-button {
  @extend .button;
  padding: 5px;
  width: 200px;
  font-size: 12px;
}
```


### レスポンシブ対応について
#### ブレイクポイント
PC用、タブレット用、スマホ用の３種類のデバイスに対応できるようにスタイルを組む。ブレイクポイントはデザイン応じて適したものを選ぶ。 <br>
以前主流だったブレイクポイントが786pxの一点のみという設計は時代遅れになりつつあるので推奨しない。<br>

#### メディアクエリはモジュール単位で記述する。
メディアクエリをブレイクポイントごとにすべてまとめて記述する方法は表示速度の点ではやや有利だが、
メンテナンス性が良くないのでモジュールごとに記述すること推奨する。<br>
Sassを使用している場合は要素ごとにミックスインをインクルードしてメディアクエリ用のスタイルを書く。
```css
/* CSSの場合 モジュールごとにメディアクエリを指定　*/
.top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 38px;
  letter-spacing: 0.04em;
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
  margin-bottom: 50px;
  padding: 10px;
  background-color: #ddd;
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
$bp-tab: 940px;
$bp-sp: 600px;

@mixin mq-tab {
  @media screen and (max-width: $bp-tab){
    @content;
  }
}

@mixin mq-sp {
  @media screen and (max-width: $bp-sp){
    @content;
  }
}

//要素ごとにミックスインをインクルードする
.top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 24px;
  letter-spacing: 0.04em;
  @include mq-tab {
    padding: 5px 0;
    font-size: 38px;
  }
  @include mq-sp {
    font-size: 22px;
  }
}

.data-list {
  margin-bottom: 50px;
  padding: 10px;
  background-color: #ddd;
  @include mq-tab {
    padding: 5px;
  }
  &__title {
    font-weight: bold;
    font-size: 24px;
    @include mq-tab {
      font-size: 20px;
    }
    @include mq-sp {
      font-size: 16px;
    }
  }
}

```

## 5. BEM(CSS設計手法)を導入する

CSSは記述の自由度が高いため、一定のルールに基づいて運用しないと簡単にカオス化してしまう。(CSS界隈では“CSS is fragile.（CSSは壊れやすい。）” という有名な格言(?)がある。)<br>
この問題は、特定のCSS設計手法を導入することによって解決できる。<br>
CSS設計手法の代表的なものには、OOCSS(オーオーシーエスエス)、SMACSS(スマックス)、BEM(ベム)と呼ばれるものがある。<br>
本スタイルガイドではBEMを推奨の基本設計手法とする。

### BEMとは？
BEMはロシアのYandex社が開発したCSSの設計手法。<br>
広く普及している設計手法なので一度覚えたら様々な場所で使うことができる。<br>

BEMではページを構成する要素を<strong>Block(ブロック)</strong>、<strong>Element(エレメント)</strong>、<strong>Modifier(モディファイア)</strong>の３種類の部品に分けて、クラスを命名する。<br>
(BEMという名前はBlock、Element、Modifierの頭文字をとったもの)<br>
- Block<br>
再利用可能な独立したパーツとして定義するもの
- Element<br>
Blockの構成要素として定義するもの。親となるブロックの内部でのみ用いる。
- Modifier<br>
BlockやElementのバリエーションとして定義するもの。見た目、状態、ふるまいなどのバージョン違いを定義する。

#### Block(ブロック)
Blockは再利用可能な独立したパーツとして定義されるもの。<br>
BlockにはできるだけBlockの利用目的に基づいて名前をつける。(例：menu、buttonなど)
```html
<!-- main-visualブロック　BEMでは単語の区切りはハイフン(ケバブケース)を用いる -->
<div class="main-visual"></div>
```
```html
<!-- 
  headerブロックとlogoブロックを定義
  ブロックの中に他のブロックがあってもよい
-->
<header class="header">
  <h1 class="logo">Example</h1>
</header>
```
#### Element(エレメント)
ElementはBlockの中身として作られる部品である。<br>
Elementを命名するときは、`block-name__element-name`というように、Block名の右に<strong>アンダースコア2つ</strong>を置いて命名する。<br>
Elementは親となるBlockの外で独立して使うことはできない。Elementは必須ではないため、Blockの中にElementを置かなくても良い。

```html
<!-- `search-form`ブロック -->
<form class="search-form">
  <!-- `search-form`ブロックの中の `input` エレメント -->
  <input class="search-form__input">
  <!-- `search-form`ブロックの中の `button` エレメント -->
  <button class="search-form__button">Search</button>
</form>
```
##### Elementのネストについて

Elementはネストして利用することができるが、Elementは必ず`block__element`という形式で、何らかのBlockに属するものとして命名される。<br>
そのため、`block__element1__element2`といった、エレメントが何か他のエレメントに属する意味になるような命名はすべきではない。
```html
<!--
  正しい。エレメント名の構造が`block__element`のパターンに従っている。
-->
<form class="search-form">
  <div class="search-form__content">
    <input class="search-form__input">

    <button class="search-form__button">Search</button>
  </div>
</form>

<!--
  間違い。エレメント名の構造が`block__element`のパターンに従っていない。
-->
<form class="search-form">
  <div class="search-form__content">
    <!-- `search-form__input` または `search-form__content-input`と書くのがよい -->
    <input class="search-form__content__input">

    <!-- `search-form__button` または `search-form__content-button`と書くのがよい -->
    <button class="search-form__content__button">Search</button>
  </div>
</form>
```

##### BlockかElementどちらをつくるべきか？
- Block - 別の場所で再利用される可能性があるものやページ内の他の要素に依存しないもの
- Element - 親となるブロックの構成要素として、親ブロックの中でしか使われないもの。

#### Modifier(モディファイア)
BlockやElementのバリエーションとして定義するもの。見た目、状態、ふるまいなどのバージョン違いを定義する。<br>
- 見た目 `size_s` `color_primary`
- 状態 `disabled` `focused`
- ふるまい `directions_left-top`

ModifierはBlockまたはElementの右に<strong>ハイフン２つ</strong>を置いて命名する。
- ブロックの場合 `block--modifier`<br>
- エレメントの場合 `block__element--modifier`

```html
<!--  `search-form`というブロックに `focused` というモディファイアを追加 -->
<form class="search-form search-form--focused">
    <input class="search-form__input">

    <!-- `search-form__button`というエレメントに`disabled`というモディファイアを追加 -->
    <button class="search-form__button search-form__button--disabled">Search</button>
</form>
```
```scss
.search-form {
  //search-formブロックのスタイルを定義
  padding: 16px;
  background-color: #fff;

  &--focused {
    // search-formブロックのバリエーションとして、
    // focusedというモディファイアのスタイルを定義
    background-color: #ffffe0;
  }

  &__button {
    //search-form__buttonエレメントのスタイル
    color: white;
    width: 180px;
    padding: 14px;
    background-color: navy;
    border-radius: 5px;
    &:hover {
      opacity: 0.8;
    }

    &---disabled {
      // search-form__buttonエレメントのバリエーションとして、
      // disabledというモディファイアのスタイルを定義
      background-color: #f4f4f4;
      color: #888;
      cursor: default;
      &:hover {
        opacity: 1;
      }
    }
  }
}

```

#### Key_value
Modifierは`key_value`という形式で定義することもできる<br>
`key`はModifierの名前、valueはModifierの値を意味する。<br>
例 `button--size_s (Modifire名：size、値:s)` `heading--color_darker (Modifire名：color、値:darker)`

```html
<!-- `search-form`というブロックに、名前が`theme`、値が`islands`のモディファイアを追加 -->
<form class="search-form search-form--theme_islands">
    <input class="search-form__input">

    <!-- `search-form__button`というエレメントに、名前が`size`、値が`m`のモディファイアを追加 -->
    <button class="search-form__button search-form__button--size_m">Search</button>
</form>
```

#### Modifierは単体では使用できない
Modifierは既存のBlockやElementのバリエーションを定義するものであるため、Modifier単体で使用することは認められない。<br>
ModifierはBlockやElementを置き換えるものではなく、見た目や状態などに変更を加えるものであるため、必ず既存のBlockやElementとのマルチクラスで用いる。

```html
<!--
    正しい。 `search-form`というブロックに`search-form--theme_islands`というモディファイアがつけられている。
-->
<form class="search-form search-form--theme_islands">
    <input class="search-form__input">
    <!-- 正しい。 `search-form__button`というエレメントに`search-form__button--size_m`というモディファイアがつけられている -->
    <button class="search-form__button search-form__button--size_m">Search</button>
</form>
```

```html
<!-- 
  間違い。変更を加えられるクラス`search-form`が抜けている
-->
<form class="search-form--theme_islands">
    <input class="search-form__input">
    <!-- 間違い。変更を加えられるクラス`search-form`が抜けている -->
    <button class="search-form__button--size_m">Search</button>
</form>
```

##### 【補足】Block or Element とModifierの区切りについて
BEMのオリジナルの記法では以下のようにBlock or ElementとModifierの区切り<strong>アンダースコア一つ</strong>でつなぐ。

###### オリジナルの記法(block__element_modifier)
```
search-form__button_size_s
```

しかし、これは少々読みにくいので、代わりに<strong>ハイフン2つ</strong>でつなげる[MindBEMding](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)と呼ばれる書き方が考案された。
こちらの記法で書くほうが読みやすいので、本スタイルガイドではこちらの記法を採用している。

###### MindBEMding記法(block__element--modifier)
```
search-form__button--size_s
```
### 「Mix」を使ってBlockとElementのスタイルを組み合わせる
Mixというテクニックを使うことで、BlockとElementのスタイルを組み合わせることができる。<br>
例えば以下のような例では、他の場所でも再利用できるような`button`というパーツそのもののスタイルはBlockとして、配置に関することなどコンテキストに依存するスタイルはElement`header__button`として記述するとよい。<br>
このようにMixを用いることでBlockの独立性を保ちつつ、Elementのクラスをミックスすることでコンテキストに応じた柔軟なスタイリングが可能になる。

```html
<div class="header">
    <!--
        `button`ブロックに`header`ブロックの`button`エレメント(=`header__button`)をミックスしているため、
        buttonブロックでありつつもheader__buttonエレメントでもある。
    -->
    <button type="button" class="button header__button"></button>
</div>
```
```scss
//汎用性のあるblockとして`button`を定義
.button {
  padding: 8px;
  width: 300px;
  border-radius: 100%;
  background-color: #333;
  color: white;
  text-align: center;
  font-size: 16px;
  &:hover {
    opacity: 0.8;
  }
}

.header {
  position: relative;
  width: 900px;
  margin: 0 auto;
 
  //特定のblock内での配置に関するスタイルはelementとして定義
  &__button {
    position: absolute;
    right: 20px;
    top: 50%;
    transform: translateY(-50%);
  }
}
```

### BEMでのセレクタのネスト（入れ子）について
BEMではネストは禁止ではないが、原則としてネストは最小限にすることを推奨している。<br>
ネストが適切な場面としては、Elementのスタイルを親となるBlockの状態に応じて変更する必要がある場合である。
```css
.button--size_s > .button__text
{
  font-size: 12px;
}
```

### さらにBEMを学ぶ
- [5分で理解するBEM](https://zenn.dev/knts0/articles/quick-understanding-bem)
- [【CSS設計】今さら聞けないBEMの基本【初心者・入門】](https://nycreation.jp/blog/archives/289)
- [BEMによるCSS設計の方法を解説。命名規則から使い方まで。](https://original-game.com/css-bem/)
- [Quick Start / Methodology BEM](https://en.bem.info/methodology/quick-start/)<br>
  BEMの公式ドキュメント。Quick Startのページだけでも目を通す価値はある。(英語が苦手な方はGoogle翻訳でどうぞ)
- 【おすすめ】[CSS設計完全ガイド(書籍)](https://gihyo.jp/book/2020/978-4-297-11173-1)<br>
  CSS設計のバイブル的な本。BEMでのHTML/CSSの書き方様々な例を上げてかなり詳しく解説されている。

### BEMから派生した設計手法
- [FLOCSS(フロックス)](https://github.com/hiloki/flocss)<br>
  [Web制作者のためのCSS設計の教科書](https://book.impress.co.jp/books/1113101128)の著者・谷 拓樹氏が考案した設計思想。<br>
  BEMの命名規則をベースに、部分的にSMACSSやOOCSSの考え方を取り入れている。<br>プロジェクトのニーズやコーダーの好みによってはこの設計手法を採用しても良い。