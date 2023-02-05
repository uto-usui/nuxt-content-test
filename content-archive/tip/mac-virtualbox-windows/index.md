---
title: "フロントエンド必須。macOSにvirtualBoxでwindows環境を構築するまで- 『front-end』"
date: "2016-10-28"
---

## macOSにvirtualBoxでwindows環境を構築する

macOSの環境に、windowsのアプリを扱いたかったり、サイトのデバッグでIEの挙動をチェックするために、windows環境をvirtualBoxを使って構築するtipsです。

### virtualBoxをダウンロード

virtualBoxはインストールしたPC上に仮想的なPCを作成し、別のOSを実行できるアプリケーションです。これでOSXの中にwindowsを立ち上げます。 [virtualBox forOSX download page](https://www.virtualbox.org/wiki/Downloads)

### winOSのパッケージをダウンロード

[Download virtual machines](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)にアクセスしてマイクロソフトのデベロッパーツールの配布ページからwinOSのパッケージをダウンロードします。

1. Virtual machineのセレクトボックスからIE8+からedgeまで選択
2. Select platformのセレクトボックスでvirtualBoxを選択
3. 選択が完了したらDownload.zipのボタンを押下

これ、かなり重たいのでめちゃくちゃ時間がかかります。 ダウンロードしたzipファイルを[The Unarchiver](https://itunes.apple.com/jp/app/the-unarchiver/id425424353?mt=12)とかで解凍するとovaファイルが格納されているので、それをvirtualBoxを起動している状態でダブルクリックします。

すると、virtualBoxの画面にインポートのダイアログが立ち上がるので、インポートを実行します。 これも結構時間かかります。

### 操作は簡単

操作はとても簡単で、パッケージをインポートすると内容が表示されるので起動ボタンを押すとウィンドウが開き、インポートしたOSが立ち上がります。 あとは普通にwindowsを操作する要領で使えます。

#### 設定で変更したい項目について

設定で詰めておきたい項目について列挙しておきます。

クリップボードの共有

設定でクリップボードを共有することができます。

仮想マシンのプロセッサー数・メモリ容量を変更

設定から割りあてているメモリやプロセッサ数を変更することができます。

キーボードの置換

デフォルトだとショートカットキーが「コマンド+c」とかで使えないので、置換してあげると快適になります。[フリーソフト 「KeySwap for ＸＰ」](http://www.asahi-net.or.jp/~ee7k-nsd/)

おわります。
