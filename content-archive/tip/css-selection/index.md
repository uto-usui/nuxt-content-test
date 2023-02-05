---
title: "テキストを選択した箇所のハイライトカラーを変更するスタイルシート -『CSS』"
date: "2016-09-16"
---

テキストを選択した箇所のハイライトカラーをCSSで変更するtipsです。

## テキストを選択している箇所のスタイルを変更する

記述は簡単で、ページ全体に指定したい場合は以下のように記述します。

#### css

```

::selection {
  background: red;
  color: white;
}
```

以下のように、セレクタを指定して絞り込むことも可能です。

#### css

```

.ex::selection {
  background: red;
  color: white;
}
```

### Mac chromeでのバグみたいなもの

2016.09現在、Mac chrome環境でのみ`::selection`セレクターの解釈が、入力変換中の文字列も対象にしてしまいます。 `input=text`とか`textarea`内などで入力中に変換すると、背景の色と`::selection`で指定した色が一致していると、一瞬文字列が消えてしまうような挙動になります。 これを避けるには先述のセレクタを指定して絞り込んでおくことが必要です。

下記のように記述します。

#### css

```

::selection {
  background: red;
  color: white;
}
input {
  background-color: white;
}
input::selection {
  color: black;
}
```

おわります。
