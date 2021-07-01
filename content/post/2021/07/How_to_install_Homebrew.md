+++
author = "sasaendo"
categories = ["How to"]
tags = ["Homebrew","コマンド"]
date = "2021-07-01"
description = "今回はPCを購入したら入れておくべきパッケージ管理であるHomebrewのインストール方法を紹介していきます。"
featured = "How_to_install_Homebrew.jpg"
featuredalt = "How to install Homebrew"
featuredpath = "/img/2021/07/"
linktitle = ""
title = "便利なパッケージ管理「Homebrew」のインストール方法を紹介"
type = "post"

+++

パッケージ管理には他にもMacPortsなどがありますが、私はHomebrewを使用しているので、きっと他のパッケージ管理より簡単なはずです！


## 目次
1. インストール方法
2. ダウンロードしておくべきコンテンツを紹介
3. 参考サイト等


## 1. インストール方法

まずHomebrewをインストールする前に以下のコマンドをターミナル（シェル）で実行します。

{{< highlight go >}}
xcode-select --install
{{< / highlight >}}

次のコマンドでPATHを通します（ファイル名を指定しただけで実行できるようにします）。

{{< highlight go >}}
sudo xcode-select --switch /Library/Developer/CommandLineTools
{{< / highlight >}}

そしたらHomebrewのインストールを行なっていきます。

{{< url-link "公式サイト" "https://brew.sh/index_ja.html" "target">}}にコマンドが載っているのでそちらをターミナルにコピぺして実行します。（以下に2021年7月1日時点のインストールコマンド載せておきます。）

{{< highlight go >}}
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
{{< / highlight >}}

処理に結構時間がかかるので、気長に待ちましょう！

Homebrewがインストールできたか以下のコマンドで確認出来ます。

{{< highlight go >}}
brew -v
Homebrew 3.1.9
Homebrew/homebrew-core (git revision a35xxxxxx; last commit 2021-06-07)
{{< / highlight >}}

これでHomebrewのインストールは終了です！

以下ではbrewコマンドで私が何をインストールしたかシェアします。

## 2. ダウンロードしておくべきコンテンツを紹介

### * Google Chrome

{{< highlight go >}}
brew install --cask google-chrome
{{< / highlight >}}

https://formulae.brew.sh/cask/google-chrome#default

### * VSCode

{{< highlight go >}}
brew install --cask visual-studio-code
{{< / highlight >}}

https://formulae.brew.sh/cask/visual-studio-code#default

### * Github

{{< highlight go >}}
brew install git
{{< / highlight >}}

https://formulae.brew.sh/formula/git#default

とりあえずはこのくらいです！

{{< url-link "公式サイト" "https://brew.sh/index_ja.html" "target">}}でインストールしたいもの検索するとインストールコマンド確認できるので、コピペでインストールできます。

最後まで見ていただきありがとうございます！

## 3. 参考サイト等

・PATHを通すとは｜「分かりそう」で「分からない」でも「分かった」気になれるIT用語辞典
https://wa3.i-3-i.info/word18471.html

・Homebrew　macOS（またはLinux）用パッケージマネージャー
https://brew.sh/index_ja.html

