# ちらしや WordPressテーマ作成 スタイルガイド
保守・カスタマイズしやすいWordPressサイトを作るためのガイド。<br>
主な注意点を挙げる。
## 静的ファイルについて  
- CSSファイル・画像・JSファイルなどの静的ファイルはワードプレスファイルの外ではなくWordPressのテーマフォルダ内に格納する。<br>
  ※後述のディレクトリ構成例も参照
- テーマフォルダ内の静的ファイルを読み込む際は、パスの指定に[get_template_directory_uri()](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_template_directory_uri)関数や[get_stylesheet_directory_uri()](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_stylesheet_directory_uri)関数（子テーマの場合）を使う。

```html
<!-- 【OK】 -->
<img src="<?php echo get_template_directory_uri(); ?>/images/logo.html">

<!-- 【NG】 get_template_directory_uri()関数を使用していない -->
<img src="/wp-content/themes/my-theme/images/logo.html">

<!-- 【NG】 静的ファイルがファイルがテーマフォルダに格納されていない -->
<img src="/images/logo.html">
```
- スタイルシートやJSファイルをテーマファイルに読み込む際は、headに直接記述せず、原則functions.phpに記述して読み込む。

```html
<!-- 【NG】header.phpのhead要素内にlinkタグやscriptタグを直接記述 -->
<head>
  <!--略-->
  <link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/style.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  <script src="<?php echo get_template_directory_uri(); ?>/js/script.js"></script>
  <!--略-->
</head>
```
```php
# 【OK】functions.phpにフックを書いてスタイルシートやスクリプトを読み込んでいる
add_action('wp_enqueue_scripts', 'my_wp_enqueue_scripts');
function my_wp_enqueue_scripts() {
  wp_enqueue_style( 'common-style', get_template_directory_uri() . '/style.css' );
  wp_enqueue_script( 'jquery' ); #WP内蔵のjQueryを使用
  wp_enqueue_script('common-script', get_stylesheet_directory_uri(). '/js/script.js', array('jquery'));
}
```
## テンプレートファイルの構成について
テーマフォルダのディレクトリ構成例の項も参照。
- 共通部分はheader.php、footer.php、sidebar.phpなどにまとめる。<br>
  header.phpには`<!DOCTYPE html>`の記述も含める。<br>
- 必要に応じてテンプレートパーツファイルを作成する。<br>
- headタグ終了直前には`wp_head()`関数、bodyタグ開始直後には`wp_body_open()`関数、bodyタグ終了直前には`wp_footer()`関数への呼び出しを必ず記述する

## 固定ページの作成
管理画面のブロックエディタで作成する固定ページは共通テンプレートのpage.phpを使えばよいが、
HTML/CSSコーディングでつくる必要のある固定ページはpage-{スラッグ名}.phpを作り、HTMLのコーディングはファイルのソースに直書きする。<br>
<strong>※HTMLのソースコードをワードプレスの管理画面の固定ページのブロックエディタや独自のカスタムフィールドから流し込むことはしない。</strong>

## テーマフォルダのディレクトリ構成例
```
my-theme/
　├─ css/
　├─ images/
　├─ js/
　├─ sass/
　├─ template-parts/
　├─ 404.php
　├─ archive.php
　├─ footer.php
　├─ front-page.php
　├─ functions.php
　├─ header.php
　├─ index.php
　├─ page.php
　├─ page-xxx.php
　├─ page-yyy.php
　├─ page-zzz.php
　├─ single.php
　└─ single-xxx.php
```
## テンプレートファイル内でのワードプレスループ  
サブループを回す場合は、原則[WP_Query](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/WP_Query)クラスを使う。query_posts関数などの非推奨関数は使わない。
WP_Queryに渡すパラーメータは、PHPの配列形式で記述する。


## カスタム投稿タイプ、カスタムタクソノミー  
<strong>Custom Post Type UI</strong>プラグインで作成する。<strong>functions.phpの記述で作成しない。</strong>

## カスタムフィールド
<strong>Advanced Cumtom Fields</strong>プラグインまたは<strong>Smart Custom Fields</strong>プラグインで作成する。<strong>functions.phpの記述で作成しない。</strong>

## お問合せフォーム  
プラグインを使う場合はContact Form 7かMW WP Formを使用する。<br>
プラグインを使用しない場合はmail.phpを使う。

## サードパーティ製のテーマをカスタマイズする場合  
必ず子テーマを作ってカスタマイズする。親テーマを直接編集しない。

## Googleアナリティクスやタグマネージャーのスクリプトの設置
メンテナンス性が悪くなるので、テンプレートファイルに直接scriptタグを記述するのはできるだけ避ける。
有料テーマの場合でテーマの設定からhead内にスクリプトを挿入できる場合は、そこから挿入する。<br>
それ以外の場合は、functions.php経由で挿入するか、[Insert Headers and Footers](https://ja.wordpress.org/plugins/insert-headers-and-footers/)などのプラグインを使用してスクリプトを挿入する。

## プラグインの導入について
利用したことがないプラグインを導入を検討する場合は以下の点に注意する。
- 最新のWordPressのバージョンと互換性があるか
- 有効インストール数が十分か
- 最終更新が古すぎないか
- そのプラグインを紹介しているブログ記事などを検索し、実際に利用したことのあるユーザーからの評判を確認する
- 稼働中のサイトに未知のプラグインを導入する場合は、本番環境でいきなり導入する前にローカル環境などで動作確認をすることを強く勧める。

## ローカル環境での開発について
新規のワードプレステーマを作成する場合や既存のワードプレステーマのテンプレートファイルに変更を加える場合は、ローカル環境で確認しながら開発するほうが効率が良い。<br>
WordPressのローカル環境構築には[Local by Flywheel](https://localwp.com/)を使うのが最も簡単でおすすめ。<br>
インストール方法や使い方は[こちらの記事](https://bazubu.com/local-by-flywheel-33920.html)が参考になる。<br>
既存のワードプレスサイトのローカルへのコピーには<strong>All-in-One WP Migration</strong>プラグインを使うと良い。<br>
使い方は[こちらの記事](https://www.webdesignleaves.com/pr/wp/wp_all_in_one_wp_migration.html)を参照。


