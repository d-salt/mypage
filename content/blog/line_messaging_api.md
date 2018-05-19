---

title: "LINE Messaging API"
date: 2018-05-03T16:20:19+09:00
categories: ["blog", "development"]
tags: ["line", "api"]
thumbnailImage: /img/blog/line.jpg
draft: false

---


LINE@のアカウントで自動応答を実現したい！  
ってことで突っ走ってみた．
<!--more-->

## とりあえず遊んでみる  
[LINE Botをサーバーレスで開発！Google Apps ScriptとLINE Messaging APIを使ってチャットボットを作ってみた - pixiv inside](https://devpixiv.hatenablog.com/entry/2016/11/14/150000)を参考に実装．

おぉ，動く．  
オウム返しだ．  

Googleってすごい．  

## ちょっと待て
おや...?  
LINE@のiOSアプリの様子がおかしいぞ...?  

ログアウトしてる．  
**アカウントが消えてる...!?**  


そうだ，これはテストだからこのMessaging APIを抹消してなかったことにしよう．  

...ん?  
消せ...ない...だと...?  

**オワタ＼(^o^)／**  


**本番が動いてるアカウントを壊した**  


さーて，これからどうしようかな...  


みなさん，ステージング環境ってとっても大事ですよ．  


