+++
author = "Theme author"
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
* ターミナルの使い方
* Homebrewのダウンロード
* Githubアカウント作成とgitのインストール

上記を行う必要があります。

ターミナルについはググって調べてみてください。

そんなの知っているよ！

という方は 2. Homebrewのダウンロードですね。こちらも公式サイトでコマンドコピーしてターミナルでダウンロードを行うことが可能です。
一から書くと長くなるので、調べてみてください。

正常にHomebrewをダウンロードすることができたら、3. Githubアカウント作成とgitのインストールです。

事前にアカウントを作成する必要があるのでやっておきましょう。

HomebrewのコマンドでGitをインストールします。こうすることでバージョンが扱いやすくなります。

Gitのコマンド等については説明省きます。


## 2.Hugoのインストール方法

次のコマンドでインストールを行います。

> brew install hugo

正常にコマンドが終了すればインストール完了です。

## 3. プロジェクト立ち上げ

次にhugoのコマンドでプロジェクトを作成していきます。

> hugo new site 任意の名称

割と任意の場所で良いみたいです。私は今後のことも考えてSSDの中でフォルダを掘って作成しました。

正常にコマンドが終了すれば、これでOKです！


## 4. GitコマンドでHugoのテーマを実装

まずは作成したプロジェクト直下で以下のコマンドを実行します。

> git init

こちらを行わないと以下のコマンドが使えません。

その後、{{< url-link "Hugoのテーマ一覧" "https://themes.gohugo.io/" "target">}}より好きなテーマを選びます。
私は今回{{< url-link "こちら" "https://themes.gohugo.io/future-imperfect/" "target">}}を選びました。

好みのテーマが見つかったら、

> cd themes

でthemesに移動して、サブモジュールとして追加します。

> git submodule add https://github.com/jpescador/hugo-future-imperfect

git submodule add の後は選んだテーマのgithubのURLになります。

ここまでくれば後は設定やコンテンツを作成するだけです！

私はイチからできる気がしなかったので既存のものをベースに使うことにしました。

おそらくthemesフォルダにいると思うので、プロジェクト直下に戻ります。

> cd ..

その後以下のコマンドを実行。

> cp -r  themes/hugo-future-imperfect/exampleSite/* .

この後プロジェクト直下のconfig.tomlを修正して、余分な.mdファイルを削除したり記事追加を行いました。

ローカル上で動かしてみます。

> hugo server

以下のURLで確認できます。

(http://localhost:1313/)
 

 確認できましたか？
 
 それではいよいよWEBに公開してみましょう！

## 5. NetlifyでWEBに公開

まずはGithubでリモートリポジトリを作成します。

{{< img-post path="img/2021/06/" file="Github01.jpg" alt="Githubリモートリポジトリ作成" >}}

> git git remote add origin git@github.com:作成したリモートリポジトリ

> git remote add origin git@github.com:作成したリモートリポジトリ

そして以下でプッシュします。

> git push origin master

これで紐付けが完了したので、次からは以下の流れでプッシュできます。

> git add -A

>　git commit -m "コミットコメント"

> git push origin master

gitの使い方を軽くレクチャーしたところでやっと、{{< url-link "Netlify" "https://www.netlify.com/" "target">}}です！

まずはアカウントを作成して、Create siteのページが現れるかと思います。

{{< img-post path="img/2021/06/" file="Netlify01.jpg" alt="Netlifyサイト作成" >}}



