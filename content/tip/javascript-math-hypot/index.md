---
title: "２点間の距離を求める関数 Math.hypot() -『JavaScript』"
date: "2018-02-05"
---

アニメーションなどインタラクティブコンテンツを実装するときなどに、よく２転換の距離を求めることがあります。 `(x0, y0)` と `(x1, y1)` の距離を求めるということです。

ES6 から用意された、`Math.hypot()` 関数を利用します。

```
const distance = (x0, y0, x1, y1) => Math.hypot(x1 - x0, y1 - y0);
distance(1, 1, 2, 3);

```

IEではサポートされていないので、必要に応じてポリフィルを定義します。

```
Math.hypot = Math.hypot || () => {
  let y = 0;
  let length = arguments.length;

  for (var i = 0; i < length; i++) {
    if (arguments[i] === Infinity || arguments[i] === -Infinity) {
      return Infinity;
    }
    y += arguments[i] * arguments[i];
  }
  return Math.sqrt(y);
};

```

- [Math.hypot() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Math/hypot)

おわります。
