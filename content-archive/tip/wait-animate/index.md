---
title: "CSSのkeyframesアニメーションで待機時間を指定したものを吐き出す WAIT! Animate - 『animation』"
date: "2016-07-13"
---

## 待機アニメーションを簡単に実装できる

WAIT! Animateは `keyframes` のCSSアニメーションでループさせたいときに、待機時間を指定したものをCSSコードとして吐き出すツールです。 遅らせたい時間を入力すると `keyframes` のタイミングを自動計算してコードをコピぺできます。

sass環境を構築していれば `mixin` をそのまま利用して、`@include` で呼び出して利用するという手もあり、このパターンでとても重宝します。

[WAIT! Animate](http://waitanimate.eggbox.io/#/)
