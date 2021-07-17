+++
author = "sasaendo"
categories = ["blog","How to"]
tags = ["Hugo","CSS","HTML","見出し",""]
date = "2021-07-17"
description = "今回はHugoで見出しの変更の為に、CSSは編集したので方法をシェアします。"
featured = "How_to_edit_css_for_Heading.jpg"
featuredalt = "How to edit css for Heading"
featuredpath = "/img/2021/07/"
linktitle = ""
title = "HugoのテーマでCSSを編集して、見出しデザインを変更する方法"
type = "post"

+++

今回は「私のブログ見出しがものすごく見辛いな」と思っていたので、CSS等カスタマイズしたので、その方法を紹介します。

## 目次
1. CSSを新規作成
2. HTMLの編集
3. TOMLファイルの修正
4. CSSの編集
5. 参考サイト

## 1. CSSを新規作成

まずはカスタムCSSファイルを作成します。

今回は見出しの編集をしたかったので、static>css>の直下にcustom_heading.cssを作成しました。

配置場所は以下のようなイメージです。

{{< highlight go >}}
ご自身のブログ-|-aechetypes
             |-content
             |-data
             |-layouts
             |-public
             |-static-|-css-|-custom_heading.css
{{< / highlight >}}

## 2. HTMLの編集

次にHTMLファイルを編集します。

今回は、single.htmlを編集していきます。

まずテーマの中にあるsingle.htmlをlayoutsにコピーします。

私は_defaultとpostの直下にあるsingle.htmlを編集したかったので、以下のような配置になりました。

{{< highlight go >}}
ご自身のブログ-|-aechetypes
             |-content
             |-data
             |-layouts-|-_default-|-single.html
		                   |-post-|-single.html
             |-public
             |-static
{{< / highlight >}}

どちらのsingle.htmlもdiv要素のidがcontentがあったので、以下のように追加しました。

{{< highlight go >}}
<div id="content">
  {{ range .Site.Params.customCSS }}
    <link rel="stylesheet" href="{{ . | absURL}}">
  {{ end }}
</div>
{{< / highlight >}}

ここまでできたら、一旦tomlファイルを編集していきます。

## 3. TOMLファイルの編集

config.tomlを編集します。

[params]にcustomCSSを配置して、先ほど作成したCSSファイルを有効にします。

大体のテーマではcustomCSSは元々あると思います。

customCSSに"/css/custom_heading.css"を追加します。

私の場合は以下のようになりました。

{{< highlight go >}}
[params]
customCSS= ["default", "/css/custom_heading.css"]
{{< / highlight >}}

## 4. CSSの編集

有効になったところで、新規に作成したcustom_heading.cssを編集していきます。

今回は初心者に優しいサイトである{{< url-link "サルワカさん" "https://saruwakakun.com/" "target">}}が提供してくれているコードを使用します。

とっても便利なので是非使って下さい。

### ＜参考サイト＞

・CSSのコピペだけ！おしゃれな見出しのデザイン例まとめ68選( {{< url-link "https://saruwakakun.com/html-css/reference/h-design" "https://saruwakakun.com/html-css/reference/h-design" "target">}} )


custom_heading.cssには以下のように編集しました。

{{< highlight go >}}
#content h2 {
    color: #66CDAA;/*文字色*/
    /*線の種類（点線）2px 線色*/
    border-bottom: dashed 2px #66CDAA;
  }
{{< / highlight >}}

idであるcontentのh2のみに適用するようにしました。

これで現在の見出しレイアウトが完成です！

最後までお読みいただきありがとうございます！

## 5. 参考サイト

・HugoでCSSを編集し、見出しのデザインを変える

  https://saruwakakun.com/html-css/reference/h-design
