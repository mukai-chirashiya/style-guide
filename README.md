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
id名やクラス名に複数単語からなる語を当てる場合、単語の区切りにはハイフンを用いる。
```html
<!--OK(ハイフンつなぎ(ケバブケース))-->
<h1 class="top-level-heading">ちらし屋ドットコム</h1>

<!--NG(大文字つなぎ(キャメルケース))-->
<h1 class="topLevelHeading">ちらし屋ドットコム</h1>

<!--NG(アンダースコアつなぎ(スネークケース))-->
<h1 class="top_level_heading">ちらし屋ドットコム</h1>
```

### クラス名やid名はできるだけ一般的な名前をつけ、名前の短さよりもわかりやすさを優先する
```html
<pre class="prettyprint">
<!--OK(長くてもわかりやすさ優先)-->
<button class="hamburger-button" id="hamburger-button"></button>

<!--OK(略語でもすぐに意味がわかるものはOK)--->
<button class="ham-button" id="ham-button"></button>

<!--NG(hbが何を意味するのかわかりづらい)-->
<button class="hb" id="hb"></button>
</pre>
```

### ローマ字での命名はしない
```
OK：heading image<br>
NG：midashi gazou
```

## CSSのスタイルガイド
### CSSのフォーマット
```css
.selector { 　　/* セレクター名(.selector)と{の間はスペースを一つ空ける */
  font-size: 16px;  /* プロパティ名(font-size)の後ろのコロン(:)と値(16px)の間はスペース１つ空ける */
  letter-spacing: 0.1em;
}　/* 閉じカッコは新しい行に入れる */
   /* 新たなセレクタを書くときは１行空ける */
.selector-foo,  /* 複数セレクタを指定する場合は改行をする */
.selector-bar,
.selector-baz {　
  margin: 0; 
  padding: 0;
}
```

### 適宜コメントを入れる
スタイルが何のためのものなのか、CSSファイルに適宜コメントを書くようにする。

#### 例
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
