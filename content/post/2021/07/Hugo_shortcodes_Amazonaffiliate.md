+++
author = "sasaendo"
categories = ["blog","How to"]
tags = ["Amazon","アフィリエイト","アフィリエイトリンク","Hugo"]
date = "2021-07-09"
description = "今回は先日HugoのThemeでAmazonアフィリエイトリンクを記事に埋め込めるように実装したので、どのようにし実装したのか紹介していきます。"
featured = "Hugo_shortcodes_Amazonaffiliate.jpg"
featuredalt = "Hugo shortcodes Amazonaffiliate"
featuredpath = "/img/2021/07/"
linktitle = ""
title = "HugoでAmazonアフィリエイトリンクを画像も含めて表示する方法"
type = "post"

+++

今回はHugoのThemeでAmazonアフィリエイトリンクを記事に埋め込めるように実装したので、その方法をシェアします。


## 目次
1. HTMLを作成する
2. 記事に商品リンクを埋め込む
3. 参考サイト

## 1. HTMLを作成する

layouts>shortcodesの直下にamazon.htmlを作成します。

配置場所は以下のようなイメージです。

{{< highlight go >}}
ご自身のブログ-|-aechetypes
             |-content
             |-data
             |-layouts-|
                       |-shortcodes-|
                                     |-amazon.html
             |-public
             |-static
{{< / highlight >}}

amazon.htmlの中身は以下です。

{{< highlight go >}}
<div class="amazon-box">
  <div class="three columns amazon-image">
    <a href="{{ .Get "url" }}" target="_blank">
      <img border="0" src="{{ .Get "imageUrl" }}">
    </a>
  </div>
  <div class="nine columns amazon-info">
    <a href="{{ .Get "url" }}" target="_blank">
      <p class="amazon-name">{{ .Get "title" }}</p>
    </a>
    <div>
    {{ .Get "summary" }}
    </div>
    <form>
      <input type="button" value="amazon" onClick="window.open('{{ .Get "url" }}','null')">
    </form>
  </div>
  <br>
</div>
{{< / highlight >}}

{{< highlight go >}}
{{ .Get "○○" }}
{{< / highlight >}}

で、以下で記載する記事内の情報と紐付けます。

レイアウトはHugoのThemeがよしなにやってくれますが、気になる方はCSSを作成してもいいかもしれません。

私も作成したらまた共有しますね！

## 2. 記事に商品リンクを埋め込む

HTMLが完成したら、

記事に以下を追加します。(※ 実際に使う際は、＜＞は半角にしてお使いください。)

{{< highlight go >}}
{{＜amazon
  url=""
  title=""
  summary=""
  imageUrl=""
 ＞}}
{{< / highlight >}}

一つ一つみていきましょう。

{{< highlight go >}}
  url=""
{{< / highlight >}}

アマゾンアフィリエイトで取得したURLここに貼り付けます。

例えば以下のURLですね！

{{< img-post path="/img/2021/07/" file="Amazonaffiliate01.jpg" alt="Amazonアフィリエイト＿テキスト" >}}

こちらのURLを先程のテンプレに貼り付けると、以下のようになります。

{{< highlight go >}}
{{＜amazon
  url="https://amzn.to/3AGAbM4"
  title=""
  summary=""
  imageUrl=""
 ＞}}
{{< / highlight >}}

次に

{{< highlight go >}}
  title=""
{{< / highlight >}}

です。

こちらは、そのままタイトルを入れればOKなので下記のように貼り付けます。

{{< highlight go >}}
{{＜amazon
  url="https://amzn.to/3AGAbM4"
  title="［デザイン技法図鑑］ひと目でわかるレイアウトの基本。"
  summary=""
  imageUrl=""
 ＞}}
{{< / highlight >}}

サマリーですが、今回は不要としたいのでそんな時はただ消してしまいます。

{{< highlight go >}}
{{＜amazon
  url="https://amzn.to/3AGAbM4"
  title="［デザイン技法図鑑］ひと目でわかるレイアウトの基本。"
  imageUrl=""
 ＞}}
{{< / highlight >}}

最後に大切な画像の部分です。

{{< highlight go >}}
  imageUrl=""
{{< / highlight >}}

ここが一番ややこしいと私は思っています笑

まず以下の要領で画像リンクが生成されるのでこちらをコピーします。

{{< img-post path="/img/2021/07/" file="Amazonaffiliate02.jpg" alt="Amazonアフィリエイト＿画像" >}}

{{< highlight go >}}
<a href="https://www.amazon.co.jp/dp/B07Y9VJ1SV?psc=1&pd_rd_i=B07Y9VJ1SVp13NParams&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUEzSk9MWk00OUU0WkpEJmVuY3J5cHRlZElkPUExMDE1MjQxNVowMFZBRllMVUNBJmVuY3J5cHRlZEFkSWQ9QTNQSEdZS1RDNUVUVUMmd2lkZ2V0TmFtZT1zcF9kZXRhaWwyJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ%3D%3D&linkCode=li2&tag=awesome3600a-22&linkId=52981e449c875b60860c7481510c6a2b&language=ja_JP&ref_=as_li_ss_il" target="_blank"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B07Y9VJ1SV&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=awesome3600a-22&language=ja_JP" ></a><img src="https://ir-jp.amazon-adsystem.com/e/ir?t=awesome3600a-22&language=ja_JP&l=li2&o=9&a=B07Y9VJ1SV" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
{{< / highlight >}}

この中で欲しいのは、aタグ内のimgタグの中のsrc=””内になるので、上記だと以下の部分になります。

{{< highlight go >}}
//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B07Y9VJ1SV&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=awesome3600a-22&language=ja_JP
{{< / highlight >}}

そしたら上記を以下に貼り付けるだけ！

{{< highlight go >}}
{{＜amazon
  url="https://amzn.to/3AGAbM4"
  title="［デザイン技法図鑑］ひと目でわかるレイアウトの基本。"
　imageUrl="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B07Y9VJ1SV&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=awesome3600a-22&language=ja_JP"
 ＞}}
{{< / highlight >}}

これで記事に記載すれば、以下のように表示されるはずです。

{{<amazon
  url="https://amzn.to/3AGAbM4"
  title="［デザイン技法図鑑］ひと目でわかるレイアウトの基本。"
  imageUrl="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B07Y9VJ1SV&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=awesome3600a-22&language=ja_JP"
 >}}

これでAmazonアフィリエイトリンクの埋め込み方法は完了です。

最後まで見ていただきありがとうございました！

## 3. 参考サイト

* Hugoのブログ用にamazonのアフィリエイトリンクのShortcodesを作った

    https://it-omurice.tokyo/post/20200308_hugo_shortcodes/


