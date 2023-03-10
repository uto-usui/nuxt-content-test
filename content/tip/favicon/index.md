---
title: "「2016版」ファビコンを必要最低限設置するまでのまとめ - 「HTML5」"
date: "2016-08-18"
---

## ファビコンの作り方

ブラウザのタブや履歴、お気に入り、ホーム画面に置いたときのショートカットアイコンとして使う、ファビコンの作成まとめです。

多くのデバイスや環境に対応しようと思うと、色々なサイズや形式のファイルを用意する必要がありますが、今回は効率的にツールを使いつつ最低限必要なものだけを設置するまとめです。

### 260x260で大きめに作成

まず大きめのサイズで雛形となるファビコンを260x260のpng形式で作成します。 ただしこれは最小で16x16のサイズで表示されるので、それを考慮して縮小して表示を確認します。 小さく表示されると細かいディティールは潰れてしまうことが多いので注意します。

### icoファイルの作成

ファビコンの拡張子は、ico形式とpng形式を用意します。

#### ico形式

ico形式は複数枚の画像データを保持できることから、マルチアイコンと呼ばれています。 ブラウザやデバイスがマルチアイコンから判断して最適なサイズのアイコンを使用します。

### favicon generatorで一括生成

[様々なファビコンを一括生成。favicon generator](http://ao-system.net/favicongenerator/) で、260x260のサイズの画像を変換して、様々なブラウザやデバイス用のファビコンを一括で生成します。

### alphaiconでマルチアイコンを生成

[半透過マルチアイコンやファビコン(favicon.ico)作成 ギザギザの無い美しい影を持ったアイコンが作成できます。](http://ao-system.net/alphaicon/)

で、先ほど一括生成したアイコンの中から「16x16」「32x32」「152x152」をマルチアイコン化(ico形式に)します。

### headタグ内に記述して設置

マルチアイコン化したファビコン(ico形式)と、ショートカット用のアイコンの中からapple-touch-icon.pngを`&lt;head&gt;`内に設置します。

#### html

```

<head>
<link rel="shortcut icon" href="assets/images/favicon.ico">
<link rel="apple-touch-icon-precomposed" href="assets/images/apple-touch-icon.png">
</head>
```

おわります。
