---

title: "Hello, hugo!"
date: 2018-05-01T19:39:08+09:00
categories: ["blog", "development"]
tags: ["development", "blog", "hugo"]
thumbnailImage: http://bepsays.com/assets/img/hugo.png
draft: false

---

<!-- # Hello, hugo! -->

作りっぱなしで放置したブログどうしようかなー  
WordPress使うのは嫌だし，CMS自分で作るかー  
なんて調べてたら**スタティックサイトジェネレータ**なるものに出会った．  
さくっと見た感じ，Goベースの[Hugo](https://gohugo.io/)が一番イケてそうだったので導入してみた．
<!--more-->

導入は，主に[サイトジェネレータ「HUGO」を使って静的サイトを作成しよう - LIG](https://liginc.co.jp/235567)を参考にした．  
（テーマは全部じゃなくて必要なやつだけインストールすれば良かった．cloneに30分くらいかかった...）  

テーマは適当にググって出てきたものの中から[Tranquilpeak](https://themes.gohugo.io/hugo-tranquilpeak-theme/)にした．  


# つまづいたところ  
## Hugoのインストール編  
* テーマは全部cloneしなくて良い．数が多すぎて時間がかかる．  

## テーマの編集編  
* 設定ファイルをjsonで書こうと思ったが上手く読み込めず．
  * テーマのexampleSiteの中にあるconfファイルをcpして書き換えたら成功
  * TOMLって誰やって思ったらGitHubの中の人が作った使いやすい形式らしい．（[参考](https://qiita.com/b4b4r07/items/77c327742fc2256d6cbe)）
* あれ，画像ってどこに置けばいいんだっけ？
  * static配下．（[参考](https://www-he.scphys.kyoto-u.ac.jp/member/shotakaha/dokuwiki/doku.php?id=toolbox:hugo:start#%E7%94%BB%E5%83%8F%E7%BD%AE%E3%81%8D%E5%A0%B4)）

## デプロイ編
* 下書きのママにして変更が反映されない！
  * draftはfalseにするんやで．

# 覚えておいたら便利なこと
* 投稿のファイル作成と同時にエディタを指定して開く（[参考](https://qiita.com/n0bisuke/items/4701481c3bca4df81b0b)）
`hugo new <ファイルパス> --editor="<エディタ>"`  

# さいごに
記事を書きながらプレビューしてたんだけど，保存するとブラウザが自動でリロードして即時反映されてる！イケてる！  
そして動くものを作るってやっぱりワクワクするね！  

# To Do
* 使いやすいようにガシガシカスタマイズ
  * [新規記事のテンプレート作成](https://qiita.com/n0bisuke/items/4701481c3bca4df81b0b)
  * [サムネイル画像の作成等々](https://hori-ryota.com/blog/create-shellscript-for-hugo-images/)

* よくわからないけどホスティングがどうの
  * [Netlifyでビルドを自動化](https://blog.mismithportfolio.com/web/hugo-netlify-build)
  * [Netlify CMS](https://blog.mismithportfolio.com/web/netlify-cms)

* ちゃんと作ったら既存HPと統合

# 参考
[なぜ静的サイトジェネレータが最強なのか](http://yoshi44ever.com/blog/static-site-generator-hugo/)  
