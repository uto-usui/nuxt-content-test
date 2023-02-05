---
title: "Wordpressの抜粋文の末尾の[...]を変更する -『wordpress』"
date: "2016-11-11"
---

WordPressで記事一覧やページのディスクリプションなどに抜粋文を出力することがあると思いますが、設定されている文字数を超えると表示される\[...\]を任意の文字列にかえるためのtipsです。

## Wordpressの抜粋文の末尾の\[...\]を変更する

抜粋文の末尾の文字列を変更するには以下のコードを`function.php`に記述します。`..more..`の部分を任意で変更してください。空にすることも可能です。

#### function.php

```
function my_excerpt_more_text($more) {
  return '..more..';
}
add_filter('excerpt_more', 'my_excerpt_more_text');

```

ちなみに抜粋文の長さ(文字数)を調節するには以下のコードを`function.php`に記述します。

#### function.php

```
function my_excerpt_length($length) {
  return 80;
}
add_filter('excerpt_length', 'my_excerpt_length');

```

おわります。
