---
title: "WordpressのRSSにカスタム投稿タイプを含める方法- 『wordpress』"
date: "2016-11-11"
---

WordpressのRSSはデフォルトでは投稿タイプごとにRSSを出力しています。ぼくはこれがわからなくて`http://my_domain.com/feed/`のurlで「フィードが出力されてない！プラグインのせいかな、、、なんかバージョンあげたときのバグとか、、、」って右往左往してしまい半日くらい潰れてしまいました。かなしかった。。そこでWordpressのRSSにカスタム投稿タイプを含めるtipsです。

## WordpressのRSSにカスタム投稿タイプを含める方法

WordpressのRSSは投稿タイプごとにRSSを出力する仕様になっているので以下のようなURLになります。

- `http://my_domain.com/feed/`
- `http://my_domain.com/post_type/feed/`

サイトの運用に応じて`http://my_domain.com/feed/`のメインのフィードに他の投稿タイプをまとめて配信したいことがあるかと思います。その場合は`function.php`で`add_filter`でメインのフィードに結合させます。

#### function.php

```
function my_feed_concat($vars) {
  if ( isset($vars['feed']) && !isset($vars['post_type']) ){
    $vars['post_type'] = array(
      'post_typeA',
      'post_typeB'
    );
  }
  return $vars;
}
add_filter( 'request', 'my_feed_concat' );

```

おわります。
