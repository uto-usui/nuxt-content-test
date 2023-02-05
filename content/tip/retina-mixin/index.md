---
title: "高解像度ディスプレイRetina用メディアクエリをmixinで記述する - 『Sass』"
date: "2016-06-19"
---

## Retinaディスプレイだけにスタイルを適用させたい

iPhoneなどの高解像度デバイスだけに、スタイル適用させるtipsです。

ウインドウサイズにブレイクポイントを設けて、判別していくことも簡単にできますが、 iPadProなど、大型のタブレット端末にもスマホ、タブレットと同じスタイルを当てたいときもあります。 大抵は、iOS固有のCSSのバグ(`background-attachment`とか)の回避や、画像の切り替えなどに利用します。

### mixinで記述を短く

毎回記述していると助長になってしまうので`Mixin`としてまとめておいて、必要なときに`@include`して呼び出します。

#### sass

```

@mixin retina {
  @media
    only screen and (-webkit-min-device-pixel-ratio: 2),
    only screen and (min--moz-device-pixel-ratio: 2),
    only screen and (-o-min-device-pixel-ratio: 2/1),
    only screen and (min-device-pixel-ratio: 2),
    only screen and (min-resolution: 192dpi),
    only screen and (min-resolution: 2dppx) {
    @content;
  }
}

@include retina {
  font-size: 30px;
}
```

おわります。
