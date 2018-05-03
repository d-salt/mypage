---

title: "Security Check"
date: 2018-05-03T10:28:33+09:00
categories: ["blog", "development"]
tags: ["security"]
thumbnailImage:
draft: false

---


自分でサイトを構えておいて脆弱なのは恥ずかしいのでテストしてみた．
<!--more-->


## さっそくテスト

テストには[OBSERVATORY by mozilla](https://observatory.mozilla.org/)を利用した．  
スコアはこんな感じ．  
![テスト結果1](https://gyazo.com/1514cf5fc30d787e9d39f787e81a06cf.png "テスト結果1")  
おぉ...  
低い


HTTPSこそ簡単だったが，サーバの設定はそういえば何もいじってない．  
ていうかそもそもいじれるのか...?  


...と思って調べてみた．  
**できるらしい．**  

無料でここまでできるNetlify恐るべし．


## レスポンスヘッダを書き換えてみた

[公式のドキュメント](https://www.netlify.com/docs/headers-and-basic-auth/) (Headers and Basic Authentication) によると  

> You can configure custom headers and basic auth for your Netlify site by adding a `_headers` file to the root of your site folder.  

...  

> You can also specify header rules in your `netlify.toml` file. You can create this file in the base directory of your git repository, if you don’t have one already.  

とのこと．  

サイト全体に設定したかったので，設定用のファイルっぽく後者を選択して記述した．

### X-Frame-Options

診断結果におすすめされたので，まずX-Frame-Optionsを設定することにした．  

**X-Frame-Optionsってなんだっけ??**  

> HTTP の X-Frame-Options 応答ヘッダーは、ブラウザーがページを `<frame>`, `<iframe>`, `<object>`の中に表示することを許可するかどうかを示すために使用されます。サイトはコンテンツが他のサイトに埋め込まれないよう保証することで、クリックジャッキング攻撃を防ぐためにこれを使用することができます。  
[X-Frame-Options - MDN web docs](https://developer.mozilla.org/ja/docs/Web/HTTP/X-Frame-Options)  

**クリックジャッキング攻撃...??**  

> クリックジャッキング（クリックジャック攻撃、Clickjacking、User Interface redress attack、UI redress attack、UI redressing）は、ウェブページの利用者に対し悪意をもって使用される技術の一種で、リンクやボタンなどの要素を隠蔽・偽装してクリックを誘い、利用者の意図しない動作をさせようとする手法である。  
[クリックジャッキング - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AA%E3%83%83%E3%82%AF%E3%82%B8%E3%83%A3%E3%83%83%E3%82%AD%E3%83%B3%E3%82%B0)  

なるほど．  
要するに，**他サイト上のユーザのためにする対策**ということですね．  

しましょう．  

`X-Frame-Options: DENY`  


### X-XSS-Protection

お次はこれ．  
Netlifyのレスポンスヘッダの設定例にあったので．  

**X-XSS-Protectionってなんだっけ??**  

> X-XSS-Protection は、ウェブブラウザ の XSS フィルターを有効化するためのオプションです。XSSの問題を完全に取り除くものではなく、XSSによる攻撃を緩和するためのものです。  
[X-XSS-Protection - セキュリティ](http://kaworu.jpn.org/security/X-XSS-Protection)  

**XSS...??**  
（っていうかこのサイトデザイン大丈夫なのか...??）  

> クロスサイトスクリプティングとは、ユーザのアクセス時に表示内容が生成される「動的Webページ」の脆弱性、もしくはその脆弱性を利用した攻撃方法のことです。  
[「クロスサイトスクリプティング（XSS）」とは？ - TrendMicro](https://www.trendmicro.com/ja_jp/security-intelligence/research-reports/threat-solution/xss.html)  


どうやら完全の脆弱性を取り除くことになるわけではなさそうだ．  
でも**このサイトは静的WebページなのでXSSの心配はない．**

とりあえず設定はしておく．

`X-XSS-Protection: 1; mode=block`


### X-Content-Type-Options

色々と調べている間にこんなページに出会った．世の中便利になったもんだ．  
[Webサーバで指定すべきヘッダ - Qiita](https://qiita.com/d6rkaiz/items/9f4ebad83b3437a0d2ea)  

ちょうど上から順番に来ているのでそれに従うことにした．  


もうお決まりだが...  

**X-Content-Type-Optionsってなに??**  

> The X-Content-Type-Options response HTTP header is a marker used by the server to indicate that the MIME types advertised in the Content-Type headers should not be changed and be followed. This allows to opt-out of MIME type sniffing, or, in other words, it is a way to say that the webmasters knew what they were doing.  
[X-Content-Type-Options - MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Content-Type-Options)  

ちゃんとしたドキュメントは英語しかなかった．  
IEがどうのって記事が多いんだから日本人こそ気にするべきなんじゃないか...?  
やはり日本のIT業界の未来が不安だ．  

どうやら一部のブラウザはこちらが指定したMIME typeを無視してくれちゃうらしい．  
そうなると意図した動作をしないので困ってしまう．  
そんなブラウザを服従させる設定．

ってことで設定  

`X-Content-Type-Options: nosniff`


### Content-Security-Policy

さすがにそろそろ調べるのに疲れてきた．  
セキュリティに関する知見の乏しさが露呈している．  

**Content Security Policy (CSP)...??**  

> Content Security Policy (CSP) とは、クロスサイトスクリプティング (XSS) やデータを差し込む攻撃などといった、特定の種類の攻撃を検知し、影響を軽減するために追加できるセキュリティレイヤーです。  
[Content Security Policy (CSP) - MDN web docs](https://developer.mozilla.org/ja/docs/Web/HTTP/CSP)  

主にサイト上でのコンテンツの読み込みに関するルール (Policy) を記載するものらしい．  
色々借り物のこのサイト，外部コンテンツなくしては成立しないので一旦保留．  

参考サイトとしていくつか置いておく．  
[Content Security Policy (CSP) - MDN web docs](https://developer.mozilla.org/ja/docs/Web/HTTP/CSP)  
[弊社のホームページにContent Security Policy(CSP)を導入しました - EG Secure Solutions Blog](https://blog.eg-secure.co.jp/2013/12/Content-Security-Policy-CSP.html)  


## チェック

ここまで設定してみたのだが，果たしてこの方法でレスポンスヘッダに適応されてるのだろうか．  
最初に確認すべきだったが...  

curlコマンドでヘッダを見ると，確かに設定された項目が存在したので大丈夫そう．  



## 再テスト

さて，ここまでで最低限の設定はできたはずなのでテストしてみる．

![テスト結果2](https://gyazo.com/8b0434f5365221205a4e88f93052b9c0.png "テスト結果2")  

まだBか...  
やっと落第は免れた程度だろうか．  

CSPが-25とスコアを大きく落としている．  
うーん，考えなければ．  

optionalでreferrer policyなるものがある．  
これで点数を稼いでみるか．

## レスポンスヘッダを書き換えてみた（続き）

### Referrer Policy

色々書いてあったがこのページが参考になりそう．  
[Referrerを制御する - Qiita](https://qiita.com/wakaba@github/items/707d72f97f2862cd8000)  

特に困ることもないはずだが，originのみの送信にしておく．  
他の値は必要ないだろう．  

`Referrer-Policy: origin`


### オマケ

#### Cache-Control

セキュリティと直接関係ないし，書き換えてもない．  
チェックしたときにヘッダを見て気になったので．  

この記事がわかりやすかったな．  
[セキュリティ対策としての Cache-Control ヘッダについて - 理系学生日記](https://kiririmode.hatenablog.jp/entry/20170625/1498389317)