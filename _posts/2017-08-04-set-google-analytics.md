---
layout: post
title: 作成中）JekyllウェブサイトでGoogle Analytics
updated: 2017-08-04 22:00 
categories:
 - blog
---

[JekyllとGitHub Pagesで立ち上げたウェブサイト](https://haltaro.github.io/archivers/first-post)に，[Google Analytics](https://analytics.google.com/analytics/web/provision/?authuser=0#provision/SignUp/)を導入した．

<iframe width="100%" height="480" src="https://www.youtube.com/embed/sXyS1Dd0ULM?rel=0" frameborder="0" allowfullscreen></iframe>

# 参考

* [Google アナリティクス トラッキングを設定する](https://support.google.com/analytics/answer/1008080?visit_id=1-636375329556963699-2710489376&rd=1)：本家ヘルプ．
* [Google Analytics setup for Jekyll](https://michaelsoolee.com/google-analytics-jekyll/)：Jekyllにおける設定方法について．
* [ブログにYouTubeの動画を埋め込む方法](http://techmemo.biz/web-cheat-sheet/%E3%83%96%E3%83%AD%E3%82%B0%E3%81%AByoutube%E3%81%AE%E5%8B%95%E7%94%BB%E3%82%92%E5%9F%8B%E3%82%81%E8%BE%BC%E3%82%80%E6%96%B9%E6%B3%95/)：Youtube動画の埋め込みについて．

# 手順

## 1. Google Analyticsの登録

[Google Analytics](https://analytics.google.com)から登録する．趣味で使うぶんにはデフォルト設定で十分だし，あとで変更可能．

## 2. analytics.htmlの作成

`管理 > プロパティ > トラッキング情報 > トラッキングコード`を選択．以下のようなJavaScriptスニペットをコピーし，`/_includes/analytics.html`として保存．ただし，`UA-*********-*`はトラッキングコード．

<script src="https://gist.github.com/haltaro/45500c3c134f5c48b549408b02c312c3.js"></script>

## 3. default.htmlの修正

## 4. 待機

設定が反映されるまで，30分ほどかかった．

# 感想

手順に従えば，問題なくできた．Youtube動画も埋め込めたので満足．
