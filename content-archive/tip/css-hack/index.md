---
title: "2016/CSSHACK ブラウザやユーザーエージェントごとにスタイルを適用させる方法 - 『CSS』"
date: "2016-06-03"
---

## ブラウザ別 CSS HACK

CSSへのセレクタなどの記述のみで、ブラウザ別にスタイルを適用させる方法です。 備忘録として。

#### IE

```

/* IE10- */
.sample{
  background: aquamarine;
}
/* IE10+ */
@media all and (-ms-high-contrast: none){
  .ex{
    background: aquamarine;
  }
}
```

#### Firefox

```

/* Firefox */
@-moz-document url-prefix(){
  .sample{
    background: aquamarine;
  }
}
```

#### Chrome

```

/* Chrome */
@media screen and (-webkit-min-device-pixel-ratio:0){
  .ex {
    background: aquamarine;
  }
}
```

#### Safari

```

/* Safari */
@media screen and (-webkit-min-device-pixel-ratio:0) {
  ::i-block-chrome, .ex {
    background: aquamarine;
}
```

## ユーザーエージェント別 CSS HACK

ユーザーエージェントはJavaScriptで判別(条件分岐)して、任意のクラスを挿入して対応します。 以下jQueryを利用した例です。

#### iPhone

```

/* iPhone */
if ( navigator.userAgent.indexOf('iPhone') > 0 ) {
    $(".ex").addClass("iPhone");
};
```

#### Android

```

/* Android */
if ( navigator.userAgent.indexOf('Android') > 0 ) {
    $(".ex").addClass("Android");
};
```

おわります。
