---
title: "カスタム投稿タイプのアーカイブページのリンク(URL)の出力 -『wordpress』"
date: "2017-01-02"
---

独自で投稿タイプを作成した、カスタム投稿タイプのアーカイブページのリンク(URL)の出力方法です。

## カスタム投稿タイプのアーカイブページのリンク(URL)の出力

以下の記述をテンプレートのsingleページに記述します。`get_post_type()`で自分のカスタム投稿タイプを取得して、`get_post_type_archive_link()`でアーカイブページへのリンクを取得して`echo`して出力させています。

### php

```
<a href="<?php echo get_post_type_archive_link( get_post_type() ); ?>"></a>

```

おわります。
