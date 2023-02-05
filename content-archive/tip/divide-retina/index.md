---
title: "Retinaディスプレイなどの高解像度の端末を判別して処理を実行する-『javascript』"
date: "2016-10-04"
---

## ディスプレイの解像度で条件分岐

Retinaディスプレイなどの高解像度のディスプレイに対して、jQuery（JavaScript）を使って判別する方法です。 高解像度用に画像を用意して、切り替えることなどに利用できます。 webkit系ブラウザのみで有効です。

#### javascript

```

var retina = window.devicePixelRatio;
if(retina < 2) {
  $('#ex').html('Retinaディスプレイとかの高解像度ではないんです。');
} else if(retina >= 2) {
  $('ex').html('Retinaディスプレイとかの高解像度です！');
}
```
