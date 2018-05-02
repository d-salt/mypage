---

title: "Hello, hugo! <カスタマイズ編>"
date: 2018-05-01T23:22:41+09:00
description: "{{ .Summary }}"
categories: ["blog", "development", "hugo"]
tags: ["development", "hugo"]
thumbnail: "http://bepsays.com/assets/img/hugo.png"
draft: false

---

# hugoの設定を色々変えてみた  
## 最終更新日時の自動取得
[Hugoで記事の最終更新日時をGit履歴から自動取得する方法 - Qiita](https://qiita.com/y_hokkey/items/ff6f7f41b23fd643421e)  

方法はわかったがgitディレクトリにはしてないので保留．Netlifyの設定をしたくらいにはgitレポジトリにする予定なのでその頃にはコメントアウトを外すかな．  

## 記事のテンプレート
[Hugoで新規記事を作成するときのTips的なメモ - Qiita](https://qiita.com/n0bisuke/items/4701481c3bca4df81b0b)  

[Front Matter - HUGO](https://gohugo.io/content-management/front-matter/)  

下書きであることのメリットがまだないのでdraftはデフォルトでfalseにしておく．  


# Page Bundles

[Content Organization - HUGO](https://gohugo.io/content-management/organization)を参考に色々．

* ディレクトリを分けて記事を書くことを覚えたよ！
  * こうすることでジャンル分け的なことができる．
  * ディレクトリ名によって呼ばれるarchetypeだったりlayoutが変わるので細かい設定が便利になる...?
    * という分けて新しくarchetypeとlayout配下にファイルを作ったよ．
      * layoutは[このへん](https://gohugo.io/content-management/sections/)とか[このへん](https://gohugo.io/variables/page/)が役に立ちそう．


## はまったところ
* category, archives, _index.mdがうまく表示されなくなった．テーマのlayoutを色々見たけどよくわからず...