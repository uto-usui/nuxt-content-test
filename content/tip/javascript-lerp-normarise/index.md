---
title: "線形補間とノーマライズのメソッド -『JavaScript』"
date: "2018-02-22"
---

インタラクティブなコンテンツを実装するときに利用したい、線形補間とノーマライズのメソッドの紹介です。processing でよく使う関数なのですが、Javascript でいつも自前で実装しています。

## 線形補間

0から1のまでの値を、任意の範囲に相当する値に変換する。

```
const lerp = (x, y, p) => {
    return x + (y - x) * p;
}

console.log( lerp(100, 200, Math.random()) )

```

## ノーマライズ

任意の範囲のある値を、0から1の範囲の値に変換する。

```
const norm = (x, y, p) => {
    return (p - x) / (y - x);
}

console.log( norm(1000, 1800, 1005) )

```

おわります。
