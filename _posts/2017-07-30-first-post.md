---
layout: post
title: jekyll + GitHub Pagesでウェブサイトを立ち上げた
updated: 2017-07-30 12:00 
categories:
 - blog
---

[Qiita](http://qiita.com/)に寄稿するほどではないけど，そこそこ技術的なメモが溜まってきた．これまでは[evernote](https://evernote.com/intl/jp/)を使ってきたが，数式やソースコードを書きづらい．[はてなブログ](http://hatenablog.com/)等で[Markdown](https://ja.wikipedia.org/wiki/Markdown)を書いても良いけど，手元にコンテンツが残らないのが嫌だったし，`haltaro`ドメインが取れなかった．ということで，[jekyll](https://jekyllrb-ja.github.io/)と[GitHub Pages](https://pages.github.com/)で，ウェブサイトを自作することにした．

# 参考

ググればいくらでも記事が出て来る．特に，以下を参考にさせて頂いた:bow:

* [jekyll公式ドキュメント](https://jekyllrb-ja.github.io/docs/home/)

# 手順

## 1. GitHubアカウント取得

## 2. github.ioレポジトリ作成

## 3. jekyllインストール

## 4. jekyllテーマ選定

[jekyll themes](http://jekyllthemes.org/)から，良さげなテーマを選ぶ．できるだけシンプルにしたかったことと，カテゴリ分類機能が欲しかったことから，[laobubu](https://github.com/laobubu)さんの[EasyBook](https://github.com/laobubu/jekyll-theme-EasyBook)を使わせてもらうことにした．

## 5. カスタマイズ

## 6. 動作確認

## 7. アップロード

```bash
$ git add . -A
$ git commit -m "First commit"
$ git push origin master
```

# 感想

前から気になってはいたけど，rubyとかjavascriptとかわからんし，ハードルが高そうで敬遠していた．でも，出来ないことは無かった（結構ハマったが）．それらしい形になったので，満足している．
