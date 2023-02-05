---
title: "OS X El Capitan ターミナルでコマンドを実行して不可視ファイルを表示する - 『mac』"
date: "2016-06-16"
---

Mac「OS X El Capitan 」で不可視ファイルを表示するには、ターミナルでコマンドを実行します。

### 不可視ファイルを表示する

```

defaults write com.apple.finder AppleShowAllFiles TRUE
```

### 不可視ファイルを非表示する

```

defaults write com.apple.finder AppleShowAllFiles FALSE
```

上記のコマンドを実行して、Finderをリロードすると、表示／非表示を切り替えることができます。

### Finderのリロード

```

killall Finder
```

おわります。
