---
title: "CSS Grid で使える minmax() 関数を理解する -『CSS』"
date: "2019-11-13"
---

CSS Grid で利用できる `minmax()` 関数はとても柔軟なレイアウトを可能にします。この関数は最小値と最大値をグリッドのトラック値として設定します。

```
.area {
  display: grid;
  grid-template-columns: minmax(min, max) minmax(min, max);
}

```

## minmax() 関数で使える単位

単位は次のものが使えます

- px
- %
- Flexible Length（fr）
- max-content
- min-content
- auto

### px / %

これはシンプルに他のプロパティと同じように動きます

```
.area {
  display: grid;
  grid-template-columns: minmax(50px, 50%) minmax(100px, 50%);
}

```

### Flexible Length (fr)

Flexible Length は CSS Grid で導入された fr と記述する単位です。この長さはグリッドコンテナ内の空きスペースの一部を表します。

```
.area {
  display: grid;
  grid-template-columns: minmax(100px, 1fr) 50%;
  wifth: 1000px;
}

```

上のように記述すると `minmax()` のカラムの最大値は 500px です。

### max-content

`max-content` は特殊で、理想的なサイズを指定します。コンテンツがテキストの場合、理想的な幅はテキストを折り返さないように振舞います。

```
.grid {
    display: grid;
    grid-template-columns: minmax(max-content, max-content) 1fr;
}

```

### min-content

`min-content` は `max-content` と同様に特殊なキーワードで、オーバーフローすることなく可能な限り水平方向のスペースを最小限に抑えたサイズとして振る舞います。

```
.grid {
    display: grid;
    grid-template-columns: minmax(min-content, min-content) 1fr;
}

```

### auto

`auto` は `minmax()` の最小値か最大値のどちらで使うかによって違ってきます。最小値のとき `auto` はセルができる最大の最小サイズ (`min-width` / `min-height`)として振る舞います。最大値として使用される場合、`auto` は `max-content` 値と同じです。

## レスポンシブを簡単に

`minmax()` は柔軟なレイアウトを可能にするので、Media Queries を利用しなくてもレスポンシブなスタイルを実現することができるので、いろいろなレイアウト実装を研究していきたいですね。
