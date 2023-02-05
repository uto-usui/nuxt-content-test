---
title: "フロントエンドを効率化。テンプレートエンジンEJSで監視下のファイルにグローバルのオブジェクトをJSON形式で渡す方法 - 『front-end』"
date: "2016-11-17"
---

テンプレートエンジンの「EJS」でgulpを使って監視下のファイルにグローバルのオブジェクトをJSON形式で渡すtipsです。

## EJSで監視下のファイルにグローバルのオブジェクトをJSON形式で渡す

ファイルやディレクトリの操作を行う**fs**というモジュールを使います。fsモジュールは「node.js」の標準機能で、そのメソッドの`fs.readFileSync`でファイルの同期読み込みの機能を利用します。`data:`の部分を任意のものに書き換えることでオブジェクト名を変更できます。

#### gulpfile.js

```
.pipe(ejs({data: JSON.parse(fs.readFileSync(srcDir + 'data.json'))}))

```

#### data.json

```
{
  "name": "site title",
  "description": "this is my site",
  "author": "",
  "title": "site title",
  "sepalate": " | ",
  "lang": "ja",
  "domain": "http://my-special-url.com/",
  "query": "?var=20161111",
  "developDir": "src/"
}

```

#### index.ejs

```
<title><%= data.name ></title>

```

ぼくが実務で使用しているEJSのコンパイル用のコードは下記のようになっています。

#### gulpfile.js

```
gulp.task('ejs',function(){
  gulp.src([srcDir + '/**/*.ejs','!' + srcDir + '/**/*_*.ejs'])
    .pipe(plumber({ errorHandler: notify.onError('<%= error.message %>') }))
    .pipe(ejs({data: JSON.parse(fs.readFileSync(srcDir + 'data.json'))}))
    .pipe(minifyHtml())
    .pipe(rename({extname: '.html'}))
    .pipe(gulp.dest(distDir + '/'))
    .pipe(browser.reload({ stream: true }))
    .pipe(notify('html task finished'));
});

```

- `_`のプレフィクスをつけたファイルのコンパイルを無視する
- エラーメッセージ
- JSONでオブジェクトを作成する
- htmlの圧縮
- 拡張子の変更
- ブラウザのリロード
- 官僚のメッセージ

おわります。
