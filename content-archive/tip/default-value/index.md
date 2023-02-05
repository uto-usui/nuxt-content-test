---
title: "引数が存在しない場合にデフォルト値を与える方法 - 『JS初心者』"
date: "2016-06-05"
---

## 引数を持たない関数を実行したときのデフォルト値

JavaScriptで処理を実行させる際に、関数を定義し引数をもたせます。 引数が設定されていないときの処理については、論理演算子を使うことにより、スマートにデフォルト値を与えることができます。

#### JavaScript

```

function exFunction (pass) {
  var yourPass = pass || '0000'; // nがなければ000を代入する
  console.log('your pass:' + yourPass);
}

exFunction('1234');  // 1234を出力
exFunction();        // 0000を出力
```

おわります。
