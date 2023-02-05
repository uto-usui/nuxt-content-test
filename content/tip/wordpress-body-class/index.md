---
title: "テンプレートタグbody_class()でbody要素に独自のクラス属性を付与する方法と、それ以外の方法 -『wordpress』"
date: "2016-12-26"
---

wordpressでページごとに限定したスタイルやJavaScriptの操作を加えたいとき、`<body>`にそのページに応じたクラスを割り当てる、`body_class()`を利用する場合があります。その使い方と、その他の`body`への有用なクラスのつけ方法をまとめます。

## テンプレートタグbody\_class()でbody要素に独自のクラス属性を付与する方法と、それ以外の方法

wordpressのテンプレートタグ`body_class()`を利用すると、そのページに応じたユニークなクラスが割り当てられます。

#### php

```
<body <?php body_class(); ?>>

```

以下のようなクラスが付与されることになります。

- home
- blog
- archive
- date
- single postid-(id)
- author
- category
- tag
- page-parent
- search-results

### 自分で付与するクラス名を決めたい場合

自分で考えた独自のクラス名を`body_class()`のパラメータに渡すことでそのクラス名を自動ではきだされるものに追加して`body`に反映することができます。

#### php

```
<body <?php body_class('my-class-name'); ?>>

```

### function.phpから自分で付与するクラス名を決めたい

function.phpに記述して`add_filter()`でクラスを`body`に付与することもできます。

#### function.php

```
add_filter( 'body_class', 'my_class_names' );
function my_class_names( $classes ) {
  $classes[] = 'my-class-name1 my-class-name2';
  return $classes;
}

```

#### 参考

- [テンプレートタグ/body class](http://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/body_class)

おわります。
