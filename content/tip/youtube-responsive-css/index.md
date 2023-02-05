---
title: "YouTubeやVimeoのiframeの埋め込み動画をCSSだけでレスポンシブに対応させる -『CSS』"
date: "2016-11-22"
---

YouTubeやVimeoのiframeの埋め込み動画をCSSだけでレスポンシブに対応させるtipsです。

## YouTubeやVimeoの埋め込み動画のレスポンシブ対応

HTMLの`src`属性の`exID`を任意のものに変更します。

#### html

```
<div class="movie">
  <iframe src="//www.youtube.com/embed/exID?rel=0" frameborder="0" allowfullscreen></iframe>
</div>

<div class="movie">
  <iframe src="//player.vimeo.com/video/exID" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
</div>

```

#### scss

```
.movie {
  position: relative;
  height: 0;
  padding-top: 30px;
  padding-bottom: 56.25%;
  overflow: hidden;
  //
  > iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
}

```

<iframe width="100%" height="500" src="//jsfiddle.net/yutousui/to582vcq/embedded/result,css,html/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

`iframe`の動画のアスペクト比にレスポンシブに親ボックスが可変するように`height`と`padding-top`でCSSを指定して、その親のボックスに`iframe`を絶対配置してサイズをフィットさせています。

以前のエントリーの応用といったところです。

- [背景画像の指定に多様したい、CSSで縦横比を維持してレスポンシブに対応する方法](http://webmanab-html.com/tip/resposive-background/)
- [SVGをインラインで配置するとき、IEとandroidが高さを計算しないのに対応する](http://webmanab-html.com/tip/svg-height/)
