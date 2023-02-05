---
title: "動画処理ツールFFmpegで動画(mp4)を音声(mp3)に変換する方法 -『tool』"
date: "2018-01-12"
---

動画処理の中でも定番で強力なツール [FFmpeg](https://www.ffmpeg.org/) を使って、コマンドラインからmp4をmp3に変換するtipsです。

## インストール

実行するのは、[Homebrew](https://brew.sh/) がインストールされているMacOS環境です。まずターミナルで ffmpeg をインストールします。

#### terminal

```
brew install ffmpeg --with-tools

```

## 変換

任意のディレクトリでコマンドを実行します。ディレクトリ以下の複数ファイルを一気に変換します。

#### terminal

```
cd [your directory]

```

```
find . -type f -name "*.mp4" -print0 | perl -pe 's/\.mp4\0/\0/g' | xargs -0 -I% ffmpeg -i %.mp4 -acodec libmp3lame -ab 256k %.mp3

```

### 参考

- [動画処理の定番ツール「FFmpeg」ことはじめ - Qiita](https://qiita.com/kitar/items/59f80bba2ca997e0f5e6)
- [FFmpegの動画圧縮・変換コマンドの使い方 – Mankind Inc.](http://mankindinc.jp/wp01/2018/03/14/ffmpeg%E3%81%AE%E5%8B%95%E7%94%BB%E5%9C%A7%E7%B8%AE%E3%83%BB%E5%A4%89%E6%8F%9B%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E4%BD%BF%E3%81%84%E6%96%B9/)
- [ffmpegの使い方：tech.ckme.co.jp](http://tech.ckme.co.jp/ffmpeg.shtml)

## その他のコマンド

今回は動画から音声を抜き出す動作を実行しましたが、FFmpeg では様々な動画のリソースに関する機能が用意されています。使いこなしていきたいです。

### 基本の動画変換

```
ffmpeg -i ex.mov ex.mp4

```

ただこれだと quickTime Player で再生できないので、次のオプションを渡してやります。

```
ffmpeg -i ex.mov -pix_fmt yuv420p ex.mp4

```

### 幅(1920)を基準にしたリサイズ

```
ffmpeg -i ex.mov -vf scale=1920:-1 ex.mp4

```

### 動画の圧縮

```
ffmpeg -i input.mp4 -c:v libx264 -an -pass 1 -s 1280x720 -f mp4 /dev/null && \
ffmpeg -i input.mp4 -c:v libx264  -b:v 2500k -c:a aac -pass 2 -s 1280x720 output.mp4

```

のようにシンプルなコマンドで実行することができます。

おわります。
