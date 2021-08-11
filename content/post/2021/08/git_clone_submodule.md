+++
author = "sasaendo"
categories = ["blog","How to",""]
tags = ["Git","クローン","サブモジュール","clone","sabmodule"]
date = "2021-08-11"
description = "今回はGitをクローンする際にサブモジュールを一緒にクローンする方法をシェアします。"
featured = "git_clone_submodule.jpg"
featuredalt = "git clone submodule"
featuredpath = "/img/2021/08/"
linktitle = ""
title = "Gitをサブモジュールも含めてクローンする方法"
type = "post"

+++

今回は備忘録もかねて、Gitをクローンする際にサブモジュールを一緒にクローンする方法をシェアします。

## 目次
1. Gitをサブモジュールと一緒にクローンする
2. 先にGitをクローンした後にサブモジュールをクローンする
3. まとめ

## 1. Gitをサブモジュールと一緒にクローンする

{{< highlight go >}}
$ git clone --recursive https://github.com/ユーザー/プロジェクト.git
{{< / highlight >}}

## 2. 先にGitをクローンした後にサブモジュールをクローンする

先にGitをクローンする。
{{< highlight go >}}
$ git clone --recursive https://github.com/ユーザー/プロジェクト.git
{{< / highlight >}}

その後プロジェクト直下に移動して、サブモジュールをクローンする。
{{< highlight go >}}
$ git submodule update --init --recursive
{{< / highlight >}}

## 3. まとめ

今回は備忘録なので短めですが、是非ブクマして使って下さいね！

最後まで見ていただきありがとうございます。

### 【関連記事】

* 【Git】２段階認証と個人トークンの設定方法

  https://www.awesome-360.com/post/2021/07/github_deprecation_notice_2fa/