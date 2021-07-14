+++
author = "sasaendo"
categories = ["blog","How to"]
tags = ["Github","２段階認証","個人アクセストークン","キーチェーンアクセス"]
date = "2021-07-13"
description = "GithubからDeprecation Noticeのメールが来たので、対応方法をシェアします。"
featured = "Github_deprecation_notice_2fa.jpg"
featuredalt = "Github deprecation notice"
featuredpath = "/img/2021/07/"
linktitle = ""
title = "Githubからパスワード認証が使えなくなるとメールが来たので、対応してみた"
type = "post"

+++

## 目次
1. Githubからきたメール内容
2. ２段階認証を設定
3. 個人アクセストークンを使用する
4. 例外
5. 参考サイト

## 1. Githubからきたメール内容

Githubから以下のメールが来ました。

-------------------------

Hi ユーザー名,

You recently used a password to access the repository at ユーザー名/リポジトリ名 with git using git/2.30.1 (Apple Git-130).

Basic authentication using a password to Git is deprecated and will soon no longer work. Visit {{< url-link "https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/" "https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/" "target">}} for more information around suggested workarounds and removal dates.

Thanks,
The GitHub Team

------------------------

どうやらパスワード認証が使えなくなるようですね。

メールに記載のURLに飛んでみました。

> In July, we announced our intent to require the use of token-based authentication (for example, a personal access, OAuth, or GitHub App installation token) for all authenticated Git operations. Beginning August 13, 2021, we will no longer accept account passwords when authenticating Git operations on GitHub.com.

2021年8月13日からトークンベースの認証が必須になるよう。

では早速対応していきます！

## 2. ２段階認証を設定

とりあえず、「two-factor authentication（２段階認証）」が必要なようなので、設定していきます。

1. {{< url-link "https://github.com/" "https://github.com/" "target">}}にログインした状態で、右上のプロフィール画像をクリックし、続いてSettings（設定）をクリックしてください。

{{< img-post path="/img/2021/07/" file="userbar-account-settings.png" alt="userbar-account-settings" >}}

2. 左のサイドバーでAccount security（アカウントのセキュリティ）をクリックしてください。

{{< img-post path="/img/2021/07/" file="settings-sidebar-account-security.png" alt="usettings-sidebar-account-security" >}}

3. 「Two-factor authentication（2要素認証）」の下でEnable two-factor authentication（2要素認証の有効化）をクリックしてください。

{{< img-post path="/img/2021/07/" file="enable-two-factor-authentication-dialoge.png" alt="enable-two-factor-authentication-dialoge" >}}

4. [Two-factor authentication] のページで、[Set up using an app] をクリックします。

5. リカバリコードを安全な場所に保存します。
    
    （リカバリコードは、アカウントにアクセスできなくなった場合に、再びアクセスするために役立ちます。）

{{< img-post path="/img/2021/07/" file="download-print-or-copy-recovery-codes-before-continuing.png" alt="download-print-or-copy-recovery-codes-before-continuing" >}}

6. 2要素のリカバリコードを保存したら、Nextをクリックします。

7. [Two-factor authentication] ページで、テキストメッセージを使って 2 要素認証を設定します。（※携帯電話の料金がかかる場合があります。）

8. 国コードを選択し、携帯電話番号を入力します。 入力した情報が正しいことを確認してから、[Send authentication code] をクリックします。

{{< img-post path="/img/2021/07/" file="2fa_sms_photo.png" alt="2fa_sms_photo" >}}

9. セキュリティコードが書かれたテキストメッセージが送信されます。 そのコードを 2 要素認証ページに入力し、Enable をクリックします。

{{< img-post path="/img/2021/07/" file="2fa-sms-code-enable.png" alt="2fa-sms-code-enable" >}}

これで２段階認証の設定は完了です！

## 3. 個人アクセストークンの設定

個人アクセストークンとは公式で以下のように説明されています。

> 個人アクセストークン（PAT）は、GitHub API またはコマンドラインを使用するときに GitHub への認証でパスワードの代わりに使用できます。

1. 先ほどと同様に、Settings（設定）から左サイドバーで [Developer settings] をクリックします。

{{< img-post path="/img/2021/07/" file="developer-settings.png" alt="developer-settings" >}}

2. 左のサイドバーでPersonal access tokens（個人アクセストークン）をクリックしてください。

{{< img-post path="/img/2021/07/" file="personal_access_tokens_tab.png" alt="personal_access_tokens_tab" >}}

3. [Generate new token] をクリックします。

{{< img-post path="/img/2021/07/" file="generate_new_token.png" alt="generate_new_token" >}}

4. トークンに任意の名前を付けます。

5. このトークンに付与するスコープ、すなわち権限を選択します。 トークンを使用してコマンドラインからリポジトリにアクセスするには、repo を選択します。

    私はほぼ選択しました。

6. [Generate token] をクリックします。

{{< img-post path="/img/2021/07/" file="generate_token.png" alt="generate_token" >}}

7. トークンをクリップボードにコピーします。 トークンを再度表示することはできないのでここで必ずコピーしてどこか安全な場所に情報を保存しておきましょう。

{{< img-post path="/img/2021/07/" file="personal_access_tokens.png" alt="personal_access_tokens" >}}


8. コマンドラインでトークンを使用しましょう。


{{< highlight go >}}
$ git clone https://github.com/username/repo.git
Username: your_username
Password: your_token
{{< / highlight >}}

パスワードの代わりに先ほどコピーしたトークンを使うことがポイントです。

これで設定は完了です。

## 4. 例外

git clone を行った際に、パスワードを求められないことがあります。

それはMacのキーチェーンアクセスにパスワードが保存されていることが原因です。

キーチェーンアクセスは Launchpad から選択できます。

そこからパスワード情報を削除すればOKです。

ただ私の場合はなぜかクローンした時はパスワードを求められず。

プッシュした時にユーザー名とパスワードを求められました。

これでもう心配いらないはずです。

最後まで見ていただきありがとうございます！

## 5. 参考サイト

* GithubからのDeprecation Noticeメールに対応してみる

	https://seraphimlog.com/github-deprecation-notice/

* 2 要素認証を設定する

    https://docs.github.com/ja/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication

* 個人アクセストークンを使用する

    https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token
