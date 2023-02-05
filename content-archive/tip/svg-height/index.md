---
title: "レスポンシブSVGをインラインで配置するとき、IEとandroidが高さを計算しないのに対応する -『CSS』"
date: "2016-07-18"
---

`svg`をインラインで配置するとき、サイズ指定の際に、幅の指定だけだとIEとAndroidの古いバージョンで高さが計算できなくて表示崩れを起こします。 それに対応するためのtipです。

## 親のボックスを作って絶対配置

[縦横比を維持してレスポンシブに対応するtips](http://webmanab-html.com/tip/resposive-background/)のときに述べたように、親要素の高さを`padding`でつくりそのボックスに対して、子要素として`svg`を絶対配置してやります。

#### html

```

<div class="svg-wrap">
  <svg class="svg">
    <!-- inline svg -->
  </svg>
</div>
```

#### css

```

.svg-wrap {
  position: relative;
  width: 100%;
  height: 0;
  padding-top: calc(50 / 200 * 100%); //アスペクト比の計算 calc(svgの高さ / svgの幅 x 要素の幅)
}

.svg {
  display: block;
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
}
```

これはIE固有のバグというわけでなく、SVG1.1の仕様がIEに実装されていないので、CSS2.1の仕様に沿ってフォールバックが働くことで起きている現象らしいです。

#### 参考

- 「 [asamuzaK.jp : ♪Vector Vector, please. Oh, the mess I'm in (c) UFO](http://asamuzak.jp/html/483) 」

IEやandroidは`svg`で詰みどころが多いので要注意です。 アニメーションとかでも引っかかることが多いです。 デバッグからのフォローバックや、プログレッシブエンハンスメントの概念で、クライアントと要件範囲について相談しておくことが大切ですね。

おわります。
