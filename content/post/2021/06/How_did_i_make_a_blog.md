+++
author = "sasaendo"
categories = ["blog", "How to"]
tags = ["blog", "Hugo", "Netlify", "Github", "Homebrew"]
date = "2021-06-24"
description = "HugoとNetlifyでブログを作成してみたので、その手順を紹介していきます。"
featured = "img/2014/04/pic03.jpg"
featuredalt = "Pic 3"
featuredpath = "date"
linktitle = ""
title = "hugoとNetlifyでブログを作成する方法"
type = "post"

+++

皆さんはブログを書いてみたい。始めてみたいと思ったことはありますか？

私もそうした思いがあり作成してみました！

今回は、このブログサイトを作った方法を共有していければと思います。

## 目次

1. 事前準備
2. Hugoのインストール方法
3. プロジェクト立ち上げ
4. GitコマンドでHugoのテーマを実装
5. NetlifyでWEBに公開


## 1. 事前準備

初めに
* ターミナル（シェル）の使い方
* Homebrewのダウンロード
* Githubアカウント作成とgitのインストール

上記を行う必要があります。

ターミナル（シェル）についてはググって調べてみてください。

そんなの知っているよ！

という方はHomebrewのダウンロードですね。こちらも公式サイトでコマンドコピーしてターミナル（シェル）でダウンロードを行うことが可能です。
一から書くと長くなるので、調べてみてください。

正常にHomebrewをダウンロードすることができたら、Githubアカウント作成とgitのインストールです。

事前にアカウントを作成する必要があるのでやっておきましょう。

HomebrewのコマンドでGitをインストールします。こうすることでバージョンが扱いやすくなります。

Gitのコマンド等については説明省きます。


## 2.Hugoのインストール方法

次のコマンドでインストールを行います。

{{< highlight go >}}
brew install hugo
{{< / highlight >}}

正常にコマンドが終了すればインストール完了です。

## 3. プロジェクト立ち上げ

次にhugoのコマンドでプロジェクトを作成していきます。

{{< highlight go >}}
hugo new site 任意の名称
{{< / highlight >}}

割と任意の場所で良いみたいです。私は今後のことも考えてSSDの中でフォルダを掘って作成しました。

正常にコマンドが終了すれば、これでOKです！


## 4. GitコマンドでHugoのテーマを実装

まずは作成したプロジェクト直下で以下のコマンドを実行します。

{{< highlight go >}}
git init
{{< / highlight >}}

こちらを行わないと以下のコマンドが使えません。

その後、{{< url-link "Hugoのテーマ一覧" "https://themes.gohugo.io/" "target">}}より好きなテーマを選びます。
私は今回{{< url-link "こちら" "https://themes.gohugo.io/future-imperfect/" "target">}}を選びました。

好みのテーマが見つかったら、

{{< highlight go >}}
cd themes
{{< / highlight >}}


でthemesに移動して、サブモジュールとして追加します。

{{< highlight go >}}
git submodule add https://github.com/jpescador/hugo-future-imperfect
{{< / highlight >}}

git submodule add の後は選んだテーマのgithubのURLになります。

ここまでくれば後は設定やコンテンツを作成するだけです！

私はイチからできる気がしなかったので既存のものをベースに使うことにしました。

おそらくthemesフォルダにいると思うので、プロジェクト直下に戻ります。

{{< highlight go >}}
cd ..
{{< / highlight >}}

その後以下のコマンドを実行。

{{< highlight go >}}
cp -r  themes/hugo-future-imperfect/exampleSite/* .
{{< / highlight >}}

この後プロジェクト直下のconfig.tomlを修正して、余分な.mdファイルを削除したり記事追加を行いました。

ローカル上で動かしてみます。

{{< highlight go >}}
hugo server
{{< / highlight >}}

以下のURLで確認できます。

(http://localhost:1313/)
 

 確認できましたか？
 
 それではいよいよWEBに公開してみましょう！

## 5. NetlifyでWEBに公開

まずはGithubでリモートリポジトリを作成します。

{{< img-post path="/img/2021/06/" file="Github01.jpg" alt="Githubリモートリポジトリ作成" >}}

Githubのリモートリポジトリと紐付け
{{< highlight go >}}
git remote add origin git@github.com:作成したリモートリポジトリ
{{< / highlight >}}

コミット
{{< highlight go >}}
git commit -m "コミットコメント"
{{< / highlight >}}

プッシュ
{{< highlight go >}}
git push origin master
{{< / highlight >}}

これで紐付けが完了したので、次から追加や修正した際は、以下の流れでプッシュできます。

全てをステージに追加
{{< highlight go >}}
git add -A
{{< / highlight >}}

追加・変更がステージにあるか確認
{{< highlight go >}}
git status
{{< / highlight >}}

コミット
{{< highlight go >}}
git commit -m "コミットコメント"
{{< / highlight >}}

プッシュ
{{< highlight go >}}
git push origin master
{{< / highlight >}}

gitの使い方を軽くレクチャーしたところでやっと、{{< url-link "Netlify" "https://www.netlify.com/" "target">}}です！

まずはアカウントを作成して、Create siteのページが現れるかと思います。

{{< img-post path="/img/2021/06/" file="Netlify01.jpg" alt="Netlifyサイト作成" >}}

以下のようにビルドの設定を行います。

{{< img-post path="/img/2021/06/" file="Netlify02.jpg" alt="Netlifyサイト作成" >}}

hugoのバージョンは

{{< highlight go >}}
hugo version
{{< / highlight >}}

で確認できます。

Deploy siteボタンをプッシュしてWEBへの公開が完了しました！

最後までみていただきありがとうございます！

