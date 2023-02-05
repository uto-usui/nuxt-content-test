---
title: "少し素敵な表現を試したい。さくっとパーティクルを実装するスクリプト「particler」 -『plug-in』"
date: "2016-09-13"
---

さくっとパーティクルを実装するためのスクリプトです。

#### javascript

```


// option
var particlerOptions = {

  // Amount of particles
  quantity: 20,

  // line width
  lineWidth: 0.05,

  // color of particles
  fillColor: "black",

  // sizes
  minSize: 1,
  maxSize: 3,

  // minimal line length
  minimalLineLength: 250,

  // speed
  speed: 25,

  // framerate
  frameDuration: 20,

  // background
  backgroundColor: 'transparent'
};

// initialize
var particlerExample = new Particler("particler-instance", particlerOptions);

```

#### MITライセンス

- [particler GitHub](https://github.com/bereziuk/particler)
- [particler デモページ](http://bereziuk.com/particler.html)

おわります。
