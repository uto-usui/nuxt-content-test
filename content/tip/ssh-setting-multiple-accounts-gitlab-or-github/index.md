---
title: "GitLabやGitHubで複数アカウントを持つときのssh設定-『Git』"
date: "2018-02-10"
---

GitLabやGitHubで、複数アカウントを切り替えて使用するときなど、SSHを複数用意してssh接続する種のtipsです。新しくGitlabのアカウントを増やしたいとき、ということで想定して進めていきます。

## 秘密鍵を作る

移動します。

```
cd ~/.ssh/

```

鍵を作成します。

```
ssh-keygen -t rsa -C "[your-mail-address@mail.com]" -f [your-file-name]

```

`[your-mail-address@mail.com]` と `[your-file-name]` は任意です。

作成したsshキーをコピーします。

```
pbcopy < ~/.ssh/[your-file-name].pub

```

コピーしたものを GitLab の settings でペーストし登録します。

## configの作成

.ssh ディレクトリに config というファイルを作り(.ssh/config)、エディタで以下のように記述します。

```
Host gitlab-[your-name].com
  User git
  Port 22
  HostName gitlab.com
  IdentityFile ~/.ssh/[your-file-name]
  TCPKeepAlive yes
  IdentitiesOnly yes

```

`[your-name]` は任意です。 `[your-file-name]` はsshキーを作ったときのファイルと対応させます。

接続のチェックをします。

```
ssh -T gitlab-[your-name].com

```

## クローン／登録

クローンする場合も、リモートリポジトリをローカルに登録する場合も、`git@gitlab.com` といつもしているところを `git@gitlab-[your-name].com` に書き換える必要があります。 `[your-name]` は configファイルで記述した、`[your-name]` と一致します。

### リモートリポジトリの登録

```
git remote add origin git@gitlab-[your-name].com:username/repositoryname.git

```

Github が出力してくれる URL をそのままコピペするなどして、もし、リモートレポジトリの登録を間違っていたら、一旦次のコマンドで消しましょう。

```
git remote rm origin

```

### クローン

```
git clone git@gitlab-[your-name].com:username/repositoryname.git

```

おわります。
