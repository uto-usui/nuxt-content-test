---
title: "El Capitan から High Sierra へのアップデート -『Mac』"
date: "2018-02-24"
---

長らく OS El Capitan を使っていたのですが、 Airpod や siri をどうしても使いたくなってきたので、2018年になってようやくアップデートしました。思い切ってみて Sierra を飛ばして、High Sierra に移行したときのメモです。

## gitが動かない

まず git が動きませんでした。次のようなメッセージが出ます。

```
Can't start Git: /usr/bin/git
The path to Git executable is probably not valid

```

xcode が抜け落ちたみたいなので、インストールし直してみます。

### xcode (コマンドラインツール)のインストール

コマンドラインツールの xcode をインストールします。

#### terminal

```
xcode-select --install

```

### Xcode を app store からインストール

app store で Xcode をインストールします。

### Xcode の同意書に同意

Xcode の同意書に同意しないと、/usr/bin/git は使えないので、ライセンスのコマンドを叩きます。

#### terminal

```
sudo xcodebuild -license

```

### 秘密鍵を自動で読み込ませる

SSH の秘密鍵が、macをシャットダウンするたびに入力を求めてくる、という仕様になってしまっているらしいです。これは面倒なので、 `~/.ssh/config`に`UseKeychain yes` を追記することで、これを解決します。

```
Host github.com
  UseKeychain yes
  HostName github.com
  IdentityFile ~/.ssh/github
  User git

Host gitlab.com
  UseKeychain yes
  User git
  Port 22
  HostName gitlab.com
  IdentityFile ~/.ssh/gitlab
  TCPKeepAlive yes
  IdentitiesOnly yes

```

というような感じですね。

いきなり git が使えなくなったので、ちょっと焦りましたが、これでひとまず大丈夫です。

## なくなったCLI ツールを再インストール

vue-cil と firebase-tools と create-react-app などが消えてしまっていたので、再インストールしました。

おわります。
