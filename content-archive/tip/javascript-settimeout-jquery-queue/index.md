---
title: "数秒後に処理を遅らせて実行するsetTimeout()とjQueryのqueue()の扱い方 -『javascript』"
date: "2016-12-15"
---

アニメーションなど何かの処理を遅らせて実行したいときや、前後関係をもたせたいときにJavaScriptの `setTimeout()` で実装する場合とJQueryの `delay()` と `queue()` で実装するときのtipsです。

## 数秒後に処理を実行するsetTimeout()とJQueryのqueue()の扱い方

### setTimeout()を使って処理を遅らせる

JavaScriptの`setTimeout()`を使うことで処理を遅らせることができます。`setTimeout()`は関数と時間を指定して、指定した時間が経過したとき、指定した関数を実行するメソッドです。

```
setTimeout(myfunc, time);

```

```
setTimeout(() => {
    $('.js-late').addClass('active').text('One second later');
  },
1000)

```

ちょっと応用として、時間の後に引数を与えると、関数に引数をセットできます。関数を外部化して、引数も配列として与えてみます。

```
const addClass = (className, text) => {

  $('.js-late').addClass('active').text(text);

};

const arg = ['active', 'One second later'];

setTimeout(addClass, 1000, ...arg);

```

`setTimeout` を `Promise` でラップした関数を使ってやると、待機処理に使いまわせて便利です。関数を使うときは `async` / `await` で記述するとさらに可読性がよくなります。

```
const pause = sec => new Promise(resolve => setTimeout(resolve, sec * 1000))

(async() => {
  await pause(1)
  console.log('hi 1sec')
  await pause(2)
  console.log('hi 3sec')
})()

```

### JQueryのqueue()を使って処理を遅らせる

アニメーションの遅延は`delay()`で処理できますが、そのあとの処理が`addClass()`などだと実行することができません。さらに`queue()`を使うことで遅延処理を実行することができます。

```
$('.js-late').delay(5000).queue(function(){
     $(this).addClass('active').text('Five second later');
});

```

#### sample

<iframe width="100%" height="400" src="//jsfiddle.net/yutousui/jh40L08L/embedded/js,result/dark/" allowpaymentrequest="" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

おわります。
