---
title: "キャッシュ管理プラグイン「WP Super Cache」のアンインストール手順 -『wordpress』"
date: "2017-01-22"
---

WP Super Cacheは、動的に生成されるページを予め静的ページで用意しておく事で、サイトの高速化を図るプラグインです。このプラグインを削除したり無効化する際に注意点があったのでまとめておきます。

## キャッシュ管理プラグイン「WP Super Cache」のアンインストール手順

### プラグインを停止する

1. サイドバーの設定からWP Super Cacheの設定ページ
2. キャッシングの停止
3. ステータスの更新
4. サイドバーのプラグインからインストール済みプラグイン
5. WP Super Cacheを停止
6. WP Super Cacheを削除

### wp-config.phpの記述を削除

wp-config.phpファイルの先頭の方に`//Added by WP-Cache Manager`とコメントアウトを見つける事ができるのでその行を削除します。

```
define('WP_CACHE', true); //Added by WP-Cache Manager
```

おわります。
