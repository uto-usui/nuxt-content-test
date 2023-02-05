---
title: "簡単になったいまどき2017年からのアイキャッチ画像のURLの取得と表示 -『wordpress』"
date: "2016-12-16"
---

面倒な記述になっていたアイキャッチ画像のURLの表示が簡単になりました。WordPress 4.4くらいからの追加の関数です。

## 簡単になったいまどき2017年からのアイキャッチ画像のURLの取得と表示

### `the_post_thumbnail_url()`

`the_post_thumbnail_url()`を使ってアイキャッチを表示します。引数にはサイズを指定します。

#### php

```
<img src="<?php the_post_thumbnail_url('medium'); ?>" alt="<?php the_title(); ?>">

```

### `get_the_post_thumbnail_url()`

`get_the_post_thumbnail_url()`でURLを取得します。引数にはIDとサイズを指定します。

#### php

```
<?php
  $image = get_the_post_thumbnail_url( get_the_ID(), 'large' );
  if($image) {
?>
<img src="<?php echo $image ?>" alt="<?php the_title(); ?>">
<?php } else { ?>
<img src="default.png" alt="<?php the_title(); ?>">
<?php } ?>

```

おわります。
