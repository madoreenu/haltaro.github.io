---
layout: post
title: 作成中）アドテク入門
updated: 2017-08-07 18:00 
categories:
 - x-tech
---

今更ながら，アドテクについて調べてみた．アドテクとは，Advertising Technologyの略で，広告配信の高度化に関する技術を指す．目的は，広告に関わる全プレーヤー（広告主，メディア，消費者）を幸せにすること．Real time bidding（RTB）市場は成長中であり，例えば機械学習で入札額を最適化する技術などが研究されている．

![ad]({{site.baseurl}}/images/2017-08-07-ad.jpg)

# 1. 目的

[CyberAgent，日本一やさしいアドテク教室](https://www.cyberagent.co.jp/ir/personal/adtech/)より抜粋．

> 1：広告主が求める高い広告効果を出すために，より適切な場所／人に広告を出すこと \\
> 2：メディアの広告枠販売や広告配信の効率化を実現し，収益最大化の支援をすること

# 2. 種類

対象や目的に応じて，三種類に分類できる．

## 2.a メディアの広告選択最適化

広告効果が大きい広告をいかに選択するか，という技術．

* [Ad Network](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%89%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF)：Webやアプリメディアなどの広告配信可能な媒体を多数束ねて広告を配信するネットワーク．
* [Ad Exchange](https://satori.marketing/marketing-blog/ad-technology/ad-exchange/)：広告枠を１インプレッション単位で売買するプラットフォーム．各媒体やAd Networkが持つ広告掲載枠を交換できる仕組み．**Ad Networkより大きな仕組み**．Ad Exchangeでは，広告出稿数と広告枠のバランスで，リアルタイムで広告枠の入札単価が変動する．Ad Exchangeには，様々なプラットフォームがある．
    * Double Click AdExchange：Googleが運営．世界最大のAd Exchange．2009年からサービス開始．
    * Open X Market Japan：Open X Japanとcciが提携して運営．2009年からサービス開始．
    * Microsoft Advertixing Exchange：Microsoftが運営．2013年からサービス開始．配信枠はMSNとSkype．
    * Facebook AdExchange：Facebookが運営．
    * Yild One：プラットフォーム・ワンが運営するSSPプラットフォーム．厳密にはAd Exchangeと異なるが，Ad Exchange的に利用することも可能．
* [SSP](https://smmlab.jp/?p=30268)：Supply Side Platformの略．オンライン広告において，広告枠を提供しているメディアの広告枠販売や広告収益最大化などを支援するツール．具体的な提供内容はサービスによって異なるが，主に，Ad NetworkやAd Exchangeの管理，リアルタイム入札（RTB）への対応などがある．

## 2.b 広告主の広告表現最適化

消費者一人ひとりにあった広告表現をいかに実現するか，という技術．

* DSP：DSPを使うことで，複数のアドネットワーク，アドエクスチェンジ，SSPを管理可能になる．
* RTB：
* Retargeting：
* Dynamic retargeting：

## 2.c ターゲット分析

広告に対するユーザの行動等のデータを，いかにマーケティングに活かすか，という技術．

* 広告効果計測ツール：
* Tracking：
* DMP：
* SDK：

# 3. 具体例

## 3.a RTBの入札価格決定

## 3.b 

# 参考

* [CyberAgent，日本一やさしいアドテク教室](https://www.cyberagent.co.jp/ir/personal/adtech/)：用語まとめもある．
* [SATORI, Ad Network（アドネットワーク）とは？を初心者にも分かりやすく解説します](https://satori.marketing/marketing-blog/ad-technology/ad-network/)：Ad Networkについて．
* [SATORI，Ad Exchange（アドエクスチェンジ）とは？を初心者にも分かりやすく解説します](https://satori.marketing/marketing-blog/ad-technology/ad-exchange/)：Ad Exchangeについて．
* [Qiita，広告と機械学習](http://qiita.com/fukkyy/items/b2d37b4797516d72225a)：2013年の記事だが，わかりやすい．
* [舘野啓，アドテクにおける機械学習技術](https://www.slideshare.net/ttpooh/tokyo-data-night-tokyodn)：数式がわかりやすい．
* [TechCrunch，Advertising Tech](https://techcrunch.com/advertising-tech/)：アドテク関連の最新ニュース．
