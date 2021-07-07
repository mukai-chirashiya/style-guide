# Chirashiya.com, Inc. Style Guide

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

### 既存のコードに手を加える場合はローカルルールを優先する
- コードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務め、一貫したローカルルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く。


```html
<p class="bar">BAR</p>
```
