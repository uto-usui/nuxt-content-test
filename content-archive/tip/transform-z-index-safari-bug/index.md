---
title: "transformのz軸とz-indexでややこしくなった時の対処法 - 『CSS』"
date: "2016-07-07"
---

CSSのプロパティで重なり順を指定する`z-index`がありますが、safari環境で詰んだので備忘録です。

## z-indexが効かない

safariでの現象になりますが `z-index` をしている要素に対して、 `transform` でZ軸に対してスタイルを指定していると、重なり順がうまくいかないことがあります。

### z-indexよりtransformのz軸が強い

この原因としては `z-index` で重なり順を指定していても、`transform`のz軸に指定した値に依存しているということが問題でした。

`b`というクラス属性の要素を前面に持ってきたい、という要件で考えます。 以下のコードだと`a`というクラス属性の要素が上に重なることになります。

```

.a {
  z-index: 10;
  transform: translate3d(0px, 0px, 100px);
}
.b {
  z-index: 100;
  transform: translate3d(0px, 0px, 10px);
}
```

重なり順を上にしたい`b`のZ軸の値を調整します。

```

.a {
  z-index: 10;
  transform: translate3d(0px, 0px, 100px);
}
.b {
  z-index: 100;
  transform: translate3d(0px, 0px, 200px);
}
```

これで要件が実現しました。 ただし、実装次第では前に持ってきたい要素のZ軸方向を動かすことで見た目が変わってしまうことも考えられます。 その場合は該当の要素をラップする形で上記の指定を行うなどして対応します。

おわります。
