---
title: "コピペできるフォントスタイルシート。2017年に向けたCSSで出来る最強のフォント指定をひととおりまとめ -『CSS』"
date: "2016-12-10"
---

## 2017年に向けたCSSで出来る最強のフォント指定をひととおりまとめ

CSSでのタイポグラフ表現で2017年にふさわしいベターな指定をまとめます。有用な情報やtipsがいろんなところで見てきてブラウザの対応状況も鑑みつつ、ぼくがベーシックで指定しているものをまとめていきます。

### フォントファミリー

フォントファミリーの指定は**ウェブフォントを使用する**のが、どの環境でも同じフォントで表示するということにおいてベストです。英語表記のサイトだとまさにこれで解決します。

しかし、ウェブフォントは日本語においては膨大なデータ量になってしまいますし、軽量化のためにサブセット化したとしても、実際の運用では人名をよく表記するようなサイトとかだと、イレギュラーな旧字とかに出会って再度サブセット化をすることになったりします。

- [Google Fonts + 日本語 早期アクセス](https://googlefonts.github.io/japanese/)
- [「Google Fonts+ 日本語 早期アクセス」を使ってみる](http://www.tam-tam.co.jp/tipsnote/html_css/post11498.html)

なので、言語が日本語のサイトにおいては、「ヒラギノ角ゴシック体」「ヒラギノ明朝体」「游ゴシック体」「游明朝体」「メイリオ」「Noto Sans CJK JP」などのOSのローカルのフォントを利用する事が現実的です。

#### scss

```
@font-face {
  font-family: "MyYuGothicM";
  font-weight: normal;
  src: local("YuGothic-Medium"),
       local("Yu Gothic Medium"),
       local("YuGothic-Regular");
}

@font-face {
  font-family: "MyYuGothicM";
  font-weight: bold;
  src: local("YuGothic-Bold"),
       local("Yu Gothic");
}

$font-serif: 游明朝, YuMincho, "ヒラギノ明朝 ProN W3", "Hiragino Mincho ProN", HG明朝E, "MS P明朝", "MS 明朝", Georgia, "Times New Roman", Times, serif;
$font-sans-serif-hiragino: -apple-system, BlinkMacSystemFont, "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic ProN", MyYuGothicM, YuGothic, メイリオ, Meiryo, "Noto Sans Japanese", "Noto Sans CJK JP", sans-serif;
$font-sans-serif-yugothic: -apple-system, BlinkMacSystemFont, 游ゴシック, "Yu Gothic", YuGothic, "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic ProN", メイリオ, Meiryo, "Noto Sans Japanese", "Noto Sans CJK JP", sans-serif;
$font-sans-serif: $font-sans-serif-hiragino;
$font-ie: "Helvetica", Meiryo, sans-serif;

body {
  font-family: $font-sans-serif;
  .ie & {
    font-family: $font-ie;
  }
}

```

`@font-face`でユーザーのローカルにある游ゴシックのフォントをオリジナルのフォントファミリーとして命名して指定することで、windowsのフォント細すぎて読めない現象を回避しています。

IE用として、游ゴシックの文字の下に余白ができるバグを回避するために、泣く泣く「Meirio」を指定しています。IEの判定として[「CSS Browser Selector」を利用して](http://webmanab-html.com/tip/css-browser-selector/)クラスを生成してスタイルを当てています。

#### 参考

- [モダン日本語フォント指定](https://speakerdeck.com/tacamy/modanri-ben-yu-huontozhi-ding)

### 自動文字詰め／カーニング

OpenTypeフォントでプロポーショナルメトリクス情報が含まれているフォントはweb上で自動文字詰めができます。`font-feature-settings`プロパティを利用することでカーニングを実行することができます。プロパティによって見た目が異なるので、マッチするものを選びますが、幾つかのバグも存在します。

#### バグ

iEとEdge:

text-align: justifyが効かなくなる

iOSとmacOSのSafari 10

font-feature-setting : "palt"を使うと、約物 （句読点・疑問符・括弧・アクセント）の文字間隔がおかしくなる

IEはそれなりに無視してしまおうかと思いますが、safariに関しては先ほどと同じく[「CSS Browser Selector」を利用して](http://webmanab-html.com/tip/css-browser-selector/)CSSハックで対応しておきます。

#### scss

```
body {
  font-feature-settings: "pwid";
  .safari & {
    font-feature-settings : "pkna"; // follow back -- ios10 safari10
  }
}

```

#### 参考

- [文字詰めできるCSSのfont-feature-settingsが凄い！ 日本語フォントこそ指定したい自動カーニング](https://ics.media/entry/14087)

### アンチエイリアスの設定

MacOSだけでの話になりますが、`font-smoothing`プロパティを利用することで、フォントのレンダリング方法を変えてアンチエイリアスのかけ方を変更します。

#### css

```
body {
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
}

```

このプロパティはアニメーションのちらつきをコントロールを扱うときに利用することも多いです。

#### scss

```
@mixin smoothFont() {
  backface-visibility: hidden;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
}

```

### フォントサイズとそのフォローバック

フォントサイズを決定する`font-size`の単位は原則`rem`で指定します。こうすることでルートのフォントサイズをJavaScriptなどで動的に変更すると簡単にフォントサイズの底上げを実行することができます。

ただし、`rem`に対応していないブラウザを考慮したフォローバックも必要です。`@mixin`でベースとなるフォントサイズをもとに`px`単位のプロパティも同時に出力するように処理します。同時に、これで相対的でない数値で指定することが可能になるので、デザインからフォントサイズを自分で計算する手間が省けます。

#### scss

```
@mixin fontsize($size: 14, $base: 14) {
  font-size: $size + px;
  font-size: ($size / $base) * 1rem;
}

html {
  font-size: 14px;
}

body {
  @include fontsize();
}

h1 {
  @include fontsize(20);
}

```

### まとめる

今までの指定と+aをまとめておきます。

#### SCSS

```
@font-face {
  font-family: "MyYuGothicM";
  font-weight: normal;
  src: local("YuGothic-Medium"),
       local("Yu Gothic Medium"),
       local("YuGothic-Regular");
}

@font-face {
  font-family: "MyYuGothicM";
  font-weight: bold;
  src: local("YuGothic-Bold"),
       local("Yu Gothic");
}

$font-serif: 游明朝, YuMincho, 'ヒラギノ明朝 ProN W3', 'Hiragino Mincho ProN', HG明朝E, 'MS P明朝', 'MS 明朝', Georgia, "Times New Roman", Times, serif !default;
$font-sans-serif-hiragino: -apple-system, BlinkMacSystemFont, "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic ProN", MyYuGothicM, YuGothic, メイリオ, Meiryo, "Noto Sans Japanese", "Noto Sans CJK JP", sans-serif !default;
$font-sans-serif-yu: -apple-system, BlinkMacSystemFont, 游ゴシック, "Yu Gothic", YuGothic, "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic ProN", メイリオ, Meiryo, "Noto Sans Japanese", "Noto Sans CJK JP", sans-serif !default;
$font-sans-serif: $font-sans-serif-hiragino;
$font-mono: Menlo, Monaco, Consolas, 'Courier New', monospace !default;
$font-tsukushi: 'Tsukushi A Round Gothic', '筑紫A丸ゴシック', "ヒラギノ丸ゴ ProN","Hiragino Maru Gothic ProN", -apple-system, BlinkMacSystemFont, Meiryo, メイリオ !default;
//
$font-ie: "Helvetica", Meiryo, sans-serif;

@mixin fontsize($size: 14, $base: 14) {
  font-size: $size + px;
  font-size: ($size / $base) * 1rem;
}

html {
  font-size: 14px;
}

body {
  @include fontsize();
  font-family: $font-sans-serif;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  font-feature-settings: "pwid";
  //
  .safari & {
    font-feature-settings : "pkna"; // follow back -- ios10 safari10
  }
  .ie & {
    font-family: $font-ie;
  }
}

```

#### CSS

```
@charset "UTF-8";
@font-face {
  font-family: "MyYuGothicM";
  font-weight: normal;
  src: local("YuGothic-Medium"), local("Yu Gothic Medium"), local("YuGothic-Regular");
}
@font-face {
  font-family: "MyYuGothicM";
  font-weight: bold;
  src: local("YuGothic-Bold"), local("Yu Gothic");
}
html {
  font-size: 14px;
}

body {
  font-size: 14px;
  font-size: 1rem;
  font-family: -apple-system, BlinkMacSystemFont, "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic ProN", MyYuGothicM, YuGothic, メイリオ, Meiryo, "Noto Sans Japanese", "Noto Sans CJK JP", sans-serif;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  font-feature-settings: "pwid";
}
.safari body {
  font-feature-settings: "pkna";
}
.ie body {
  font-family: "Helvetica", Meiryo, sans-serif;
}


```

おわります。
