+++
author = "sasaendo"
categories = ["blog","How to"]
tags = ["Hugo","アフィリエイトリンク","HTML","CSS","Amazon","楽天","アフィリエイト"]
date = "2021-07-23"
description = "今回はHugoテーマのブログでアフィリエイトリンクを埋め込めるように編集したので、その方法をシェアします。"
featured = "How_to_edit_affiliate_link_Hugo.jpg"
featuredalt = "How to edit affiliate link at Hugo Theme"
featuredpath = "/img/2021/07/"
linktitle = ""
title = "Hugoのブログでアフィリエイトリンクを作成する方法"
type = "post"

+++

今回は私が使用しているHugoテーマでアフィリエイトリンクを埋め込めるよう編集したので、その方法について紹介していきます。

では早速いってみましょう！

## 目次
1. HTMLを編集
2. CSSを編集
3. TOMLファイル編集
4. CSSファイル編集
5. 最後に

## 1. HTMLを編集

まずはhtmlファイルを作成します。

今回はaffiliate.htmlというファイルをshortcodes内に作成しました。

配置位置は以下の感じです。

{{< highlight go >}}
ご自身のブログ-|-aechetypes
             |-content
             |-data
             |-layouts-|
                       |-shortcodes-|
                                     |-affiliate.html
             |-public
             |-static
{{< / highlight >}}

ファイル内を編集していきましょう。

私は以下のようになりました。

{{< highlight go >}}
<div class="affiliate-box">
    <div class="three columns amazon-image">
      <a href="{{ .Get "amazon-url" }}" target="_blank">
        <img border="0" src="{{ .Get "imageUrl" }}">
      </a>
    </div>
    <div class="affiliate-info">
      <div class="amazon-info">
        <a href="{{ .Get "amazon-url" }}" target="_blank">
          <p class="amazon-name">{{ .Get "title" }}</p>
        </a>
        <div>
          <p>{{ .Get "summary" }}</p>
        </div>
      </div>
      <a href="{{ .Get "amazon-url" }}" target="_blank" id="amazon-btn" class="affiliate-btn">Amazon</a>/*Amazonのボタンリンク*/
      <a href="{{ .Get "rakuten-url" }}" target="_blank" id="rakuten-btn" class="affiliate-btn">楽天</a>/*楽天のボタンリンク*/
    </div>
    <br>
  </div>
{{< / highlight >}}

楽天のボタンリンクを増やす為に構造をイジりました。

HTMLはこれでOKです。

ではCSSを編集していきましょう。

## 2. CSSを編集

まずはcssファイルを作成しましょう。

今回は、custom_affiliate.cssというファイルをstaticフォルダのcssフォルダ直下に作成しました。

配置位置は以下の感じです。

{{< highlight go >}}
ご自身のブログ-|-aechetypes
             |-content
             |-data
             |-layouts
             |-public
             |-static-|-css-|-custom_affiliate.css
{{< / highlight >}}

一旦tomlファイルを編集します。

## 3. TOMLファイル編集

config.tomlを編集します。

[params]にcustomCSSを配置して、先ほど作成したCSSファイルを有効にします。

大体のテーマではcustomCSSは元々あると思います。

customCSSに"/css/custom_affiliate.css"を追加します。

私の場合は以下のようになりました。

{{< highlight go >}}
[params]
customCSS= ["default", "/css/custom_heading.css", "/css/custom_affiliate.css"]
{{< / highlight >}}

## 4. CSSファイル編集

有効になったところで、新規に作成したcustom_affiliate.cssを編集していきます。

custom_affiliate.cssには以下のように編集しました。

{{< highlight go >}}
.affiliate-box {
    padding: 0.5em 1em;
    margin: 2em 0;
    font-weight: bold;
    border: solid 1px rgba(160, 160, 160, 0.3);
    border-radius: 10px;/*角の丸み*/
}
.affiliate-box p {
    margin: 0; 
    padding: 0;
}

.affiliate-btn {
    position: relative;
    top: auto;
    margin: 4px;
    padding: 0 !important;
    padding-bottom: 5px !important;
    width: 7em;
    color: #ffffff;
    display: inline-block;
    border: none;
    border-radius: 6px;
    box-shadow: 0 2px 0 0 rgba(0,0,0,0.2);
    outline: none;
    text-align: center;
}

.affiliate-btn:hover {
    color: #ffffff !important;
}
 
.affiliate-btn:active {
    position: relative;
    top: 2px;
    box-shadow: none;
    color: #e2e2e2;
    outline: none;
}
 
#amazon-btn {
    background: #ff9900;
}
#rakuten-btn {
    background: #bf0000;
}

#amazon-btn:hover {
    background: #f09102;
}
#rakuten-btn:hover {
    background: #ad0000;
}
{{< / highlight >}}

私は今回、現在使用しているHugoテーマのSNSなどのシェアボタンと統一したデザインにしたかったので、そちらを参考にしました。

また、Amazonや楽天のcolorコードは以下のサイトで確認して反映させました。

### ＜参考サイト＞
* SNSやWebサービスなどのロゴの色（ブランドカラー）を調べてみた
	{{< url-link "http://weboook.blog22.fc2.com/blog-entry-399.html" "http://weboook.blog22.fc2.com/blog-entry-399.html" "target">}}

これで現在のレイアウトが完成です！

{{<affiliate
  amazon-url="https://amzn.to/3Bzycte"
  rakuten-url="https://rpx.a8.net/svt/ejp?a8mat=3HG9XA+EVU582+2HOM+BWGDT&rakuten=y&a8ejpredirect=https%3A%2F%2Fhb.afl.rakuten.co.jp%2Fhgc%2Fg00q0724.2bo11c45.g00q0724.2bo12179%2Fa21071121224_3HG9XA_EVU582_2HOM_BWGDT%3Fpc%3Dhttps%253A%252F%252Fitem.rakuten.co.jp%252Fbook%252F16084152%252F%26m%3Dhttp%253A%252F%252Fm.rakuten.co.jp%252Fbook%252Fi%252F19802122%252F"
  title="ポチらせる文章術"
  imageUrl="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=4827211965&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=awesome3600a-22&language=ja_JP"
 >}}

## 5. 最後に

今回は以前作成したAmazonアフィリエイトリンクや見出しデザイン編集の応用編になります。

色々作成しているとアイデアとか湧いてきて楽しいですね！

最後までお読みいただきありがとうございます！

### 【関連記事】

* HugoとNetlifyでブログを作成する方法

	https://www.awesome-360.com/post/2021/06/how_did_i_make_a_blog/

* HugoでAmazonアフィリエイトリンクを画像も含めて表示する方法

	https://www.awesome-360.com/post/2021/07/hugo_shortcodes_amazonaffiliate/

* HugoのテーマでCSSを編集して、見出しデザインを変更する方法

	https://www.awesome-360.com/post/2021/07/how_to_edit_css_for_heading/

