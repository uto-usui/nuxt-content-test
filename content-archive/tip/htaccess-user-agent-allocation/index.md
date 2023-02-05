---
title: "スマホ用にディレクトリを分けた構造のサイトで.htaccessでユーザーエジェントごとに振り分ける -『front-end』"
date: "2016-07-15"
---

スマホ用・PC用などユーザーのデバイスごとにアクセスさせたいURLが異なる場合、指定したディレクトリにアクセスさせるtipsです。

## 指定したディレクトリに振り分け、アクセスさせる

振り分けを行いたいディレクトリのルートに(主にドメインルート).htaccessファイルを作成し、記述します。 PCからスマホ/タブレット用URLへのアクセスがあった際に、PC用にURLを書き換えるコードは以下です。

#### .htaccess

```

RewriteEngine on

RewriteCond %{REQUEST_URI} /sp/
RewriteCond %{HTTP_USER_AGENT} !(iPod|iPhone|iPad|Android|Windows\ Phone)
RewriteRule ^sp/(.*)$ $1 [R]
RewriteBase /
```

PC

http://ex.com/

SP

http://ex.com/sp/

以上の構造のディレクトリのサイトで作成した場合のサンプルです。

また、スマホからPC用のURLに書き換える場合は以下です。

```

RewriteEngine on

RewriteCond %{REQUEST_URI} !/sp/
RewriteCond %{HTTP_USER_AGENT} (iPod|iPhone|iPad|Android|Windows\ Phone)
RewriteRule ^(.*)$ sp/$1 [R]
RewriteBase /
```

`RewriteEngine on` の記述は一度で大丈夫です。

おわります。
