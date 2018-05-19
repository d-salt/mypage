---

title: "Hello, netlify!"
date: 2018-05-02T12:02:04+09:00
categories: ["blog", "development"]
tags: ["netlify"]
thumbnailImage: /img/netlify.png
draft: false

---

<!-- # Hello, netlify! -->

こんな記事を見つけたので設定してみた．  
[NetlifyでHugoで作った静的サイトをホスティングしてビルドを自動化する - Snaplog](https://blog.mismithportfolio.com/web/hugo-netlify-build)
<!--more-->


**これはやばい**

**サーバレスで! 無料で! 独自ドメインをSSLで! 使える...!**

しかもビルドからデプロイまでを自動化できる．  
つまりhugoをインストールしたローカル環境以外からでもgithubにアクセスできれば更新できる...!

やばいっす．


記事に書いてない独自ドメインとSSLの設定は感覚でぽちぽち．  
DNSのNSの設定も表示してくれたのでその通りに設定．  
すぐに反映されました．

証明書がwwwで取られたので，wwwをプライマリドメインにしたところはちょっとつまったかな．  

ちなみに記事にあるとおりバージョンの違いで一度デプロイに失敗しました^^;


