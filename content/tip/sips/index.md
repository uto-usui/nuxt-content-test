---
title: "複数の画像を手早くsipsコマンドで一括リサイズする -『Mac』"
date: "2018-03-25"
---

画像をリサイズする退屈な作業を一括で行ったり自動化する方法はいくつかあります。フロントエンド開発ではタスクランナーを使ったり、よく使うのはPhotoshopのスクリプトを利用したりするのではないでしょうか。そこで、アプリを立ち上げるのが面倒なときに Mac のターミナルでサクッと sips コマンドでリサイズをする tips です。

Terminal を開いて cd コマンドで 任意のディレクトリに移動して、次のコマンドを実行します。

#### terminal

```
sips -Z 500 *.jpg

```

\-Z

比率を保つ

640

高さと幅の最大値

\*.jpg

拡張子の選択、画像の拡張子が .JPG であれば、ここを変更する

という簡単なコマンドで一括リサイズすることができました。今回はサムネイルを作るようなイメージですね。ぼくはカメラの大きな画像をこれでリサイズしてカメラロールのようなものを生成することにしています。

sips コマンドでは他にも色々な画像の加工ができるので、こちらを参考にどうぞ。

- [Macのターミナルで簡単に画像処理できるsipsの使い方](https://qiita.com/livlea/items/53b755e5067d4ebc5b43)

おわります。