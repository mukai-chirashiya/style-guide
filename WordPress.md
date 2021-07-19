# WordPressサイト制作ガイド
保守・カスタマイズしやすいWordPressサイトを作るためのガイド。<br>
主な注意点を箇条書きで挙げる。
## 静的ファイルについて  
    - CSSファイル・画像・JSファイルなどの静的ファイルはワードプレスファイルの外ではなくWordPressのテーマフォルダ内に格納する。<br>
      ※後述のディレクトリ構成例も参照
    - テーマフォルダ内の静的ファイルを読み込む際は、パスの指定に[get_template_directory_uri()](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_template_directory_uri)関数や[get_stylesheet_directory_uri()](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_stylesheet_directory_uri)関数（子テーマの場合）を使う。<br>

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


## テンプレートファイルの構成  
共通部分はheader.php、footer.php、sidebar.phpなどにまとめる。<br>
header.phpには`<!DOCTYPE html>`の記述も含める。<br>
必要に応じてテンプレートパーツファイルを作成する。

## テンプレートファイル内でのワードプレスループ  
サブループを回す場合は、原則[WP_Query](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/WP_Query)クラスを使う。query_posts関数などの非推奨関数は使わない。
WP_Queryに渡すパラーメータは、PHPの配列形式で記述する。

## 固定ページの作成
管理画面のブロックエディタで作成する固定ページは共通テンプレートのpage.phpを使えばよいが、
HTML/CSSコーディングでつくる必要のある固定ページはpage-{スラッグ名}.phpを作り、HTMLのコーディングはファイルのソースに直書きする。<br>
※HTMLのソースコードをワードプレスの管理画面の固定ページのブロックエディタや独自のカスタムフィールドから流し込むことはしない。

## カスタム投稿タイプ、カスタムタクソノミー  
Custom Post Type UIプラグインで作成する。functions.phpの記述で作成しない。

## カスタムフィールド
Advanced Cumtom FieldsまたはSmart Custom Fieldsで作成する。functions.phpの記述で作成しない。

## お問合せフォーム  
プラグインを使う場合はContact Form 7、MW WP Formを使用する。<br>
プラグインを使用しない場合はmail.phpを使う。

## 既成のテーマをカスタマイズする場合  
必ず子テーマを作ってカスタマイズする。親テーマを直接編集しない。

## Googleアナリティクスやタグマネージャーのスクリプトの設置
メンテナンス性が悪くなるので、テンプレートファイルに直接scriptタグを記述するのはできるだけ避ける。
有料テーマの場合でテーマの設定からhead内にスクリプトを挿入できる場合は、そこから挿入する。<br>
それ以外の場合は、functions.php経由で挿入するか、[Insert Headers and Footers](https://ja.wordpress.org/plugins/insert-headers-and-footers/)などのプラグインを使用してスクリプトを挿入する。

## テーマフォルダのディレクトリ構成例
```
my-theme/
　├─ css/
　├─ images/
　├─ js/
　├─ sass/
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


