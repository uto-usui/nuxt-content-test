---
title: "lengthプロパティで特定の要素の存在を判別して処理を実行する - 『JS / jQuery』"
date: "2016-06-05"
---

JavaScriptで特定の要素の存在を判別して処理を実行するスクリプトを記述したいときのtipsです。

## .lengthとif文

`length`プロパティで指定したjQueryオブジェクトの要素数を取得することで、要素の有無を確認できます。 それをif文で処理すると**「要素があるかどうか」**を判別する処理が実現します。

### 要素があるときだけ処理する

#### JavaScript

```

if($('#ex').length) {
  console.log('Yes');
}
```

### 要素がないときだけ処理する

#### JavaScript

```

if(!$('#ex').length) {
  console.log('No');
}
```

### 要素の有無で処理を変更する

#### JavaScript

```

if($('#ex').length) {
  console.log('Yes');
} else {
  console.log('No');
}
```

おわります。
