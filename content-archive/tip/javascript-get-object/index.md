---
title: "連想配列を列挙する -『JavaScript』"
date: "2017-12-15"
---

連想配列のkeyとvalueを取得します。

こんなオブジェクトとします。

```
let obj = {
  ruffy: {
    age: 19,
    from: east
  },
  nami: {
    age: 20,
    from: east
  },
  sanji: {
    age: 21,
    from: north
  }
};

```

## Object.entries

`Object.entries()` メソッドは、引数に与えたオブジェクトが所有する、列挙可能な `[key, value]` からなる配列を返します。

- [Object.entries() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

```
for (let [key, value] of Object.entries(obj)) {
  console.log(`key: ${key} value: ${value}`);
}

```

## Object.keys(obj).forEach

- [Object.keys() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
- [TypedArray.prototype.forEach() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/forEach)

```
Object.keys(obj).forEach(key => console.log(`key: ${key} value: ${obj[key]}`));

```

## for-in

`for-in` ループではプロトタイプチェーン内のプロパティも列挙されます。

- [for...in - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/for...in)

```
for (let key in obj) {
  console.log(`key: ${key} value: ${obj[key]}`);
}

```
