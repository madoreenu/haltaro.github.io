---
layout: post
title: 作成中）アドテク入門
updated: 2017-08-07 18:00 
categories:
 - x-tech
---

今更ながら，アドテクについて調べてみた．アドテクとは，Advertising Technologyの略で，広告配信の高度化に関する技術を指す．目的は，広告に関わる全プレーヤー（広告主，メディア，消費者）をwin-winの関係にすること．Real time bidding（RTB）市場は成長中であり，例えば機械学習で入札額を最適化する技術などが研究されている．

![ad]({{site.baseurl}}/images/2017-08-07-ad.jpg)

# 1. 目的

[CyberAgent，日本一やさしいアドテク教室](https://www.cyberagent.co.jp/ir/personal/adtech/)より抜粋．

> 1：広告主が求める高い広告効果を出すために，より適切な場所／人に広告を出すこと \\
> 2：メディアの広告枠販売や広告配信の効率化を実現し，収益最大化の支援をすること

# 2. 種類

対象や目的に応じて，三種類に分類できる．

## 2.a メディアの広告選択最適化

広告効果が大きい広告をいかに選択するか，という技術．

* [**Ad Network**](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%89%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF)：Webやアプリメディアなどの広告配信可能な媒体を多数束ねて広告を配信するネットワーク．
* [**Ad Exchange**](https://satori.marketing/marketing-blog/ad-technology/ad-exchange/)：広告枠を１インプレッション単位で売買するプラットフォーム．各媒体やAd Networkが持つ広告掲載枠を交換できる仕組み．**Ad Networkより大きな仕組み**．Ad Exchangeでは，広告出稿数と広告枠のバランスで，リアルタイムで広告枠の入札単価が変動する．Ad Exchangeには，様々なプラットフォームがある．
    * **Double Click AdExchange**：Googleが運営．世界最大のAd Exchange．2009年からサービス開始．
    * **Open X Market Japan**：Open X Japanとcciが提携して運営．2009年からサービス開始．
    * **Microsoft Advertixing Exchange**：Microsoftが運営．2013年からサービス開始．配信枠はMSNとSkype．
    * **Facebook AdExchange**：Facebookが運営．
    * **Yild One**：プラットフォーム・ワンが運営するSSPプラットフォーム．厳密にはAd Exchangeと異なるが，Ad Exchange的に利用することも可能．
* [**SSP**](https://smmlab.jp/?p=30268)：Supply Side Platform．オンライン広告において，広告枠を提供しているメディアの広告枠販売や広告収益最大化などを支援するツール．具体的な提供内容はサービスによって異なるが，主に，Ad NetworkやAd Exchangeの管理，リアルタイム入札（RTB）への対応などがある．

## 2.b 広告主の広告表現最適化

消費者一人ひとりにあった広告表現をいかに実現するか，という技術．

* [**DSP**](https://webbu.jp/dsp_mechanism-276)：Demand Side Platform．広告主はターゲットや予算を設定し，バナーを入稿するだけで，DSPが自動で最適な広告配信を行う．DSPを使うことで，複数のアドネットワーク，アドエクスチェンジ，SSPを管理可能になる．SSPのリクエストに応じて，どのような広告をいくらで入札するか決定する．つまり，広告枠のオークションが行われる．
* **RTB**：
* **Retargeting**：DSPが提供することもある．
* **Dynamic retargeting**：

## 2.c ターゲット分析

広告に対するユーザの行動等のデータを，いかにマーケティングに活かすか，という技術．

* **広告効果計測ツール**：
* **Tracking**：
* [**DMP**](https://dmlab.jp/adtech/dmp.html)：Data Management Platform．インターネットに蓄積された情報を管理し，分析結果を広告配信に利用するためのプラットフォーム．現実的には，データの蓄積は進んでいるが，データの活用については敷居が高い模様．下記の二種類がある．
    * Open DMP：データ提供会社が保有している行動履歴や属性情報．
    * Private DMP：自社独自で保有している購買履歴，興味関心情報．
* **SDK**：

# 3. 具体例

## 3.a RTBの入札価格決定

<iframe src="//www.slideshare.net/slideshow/embed_code/key/K2EnIQpqVgHKCh" width="100%" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/ttpooh/tokyo-data-night-tokyodn" title="アドテクにおける機械学習技術 @Tokyo Data Night #tokyodn" target="_blank">アドテクにおける機械学習技術 @Tokyo Data Night #tokyodn</a> </strong> from <strong><a href="https://www.slideshare.net/ttpooh" target="_blank">Kei Tateno</a></strong> </div>

## 3.b 

# 参考

* [CyberAgent，日本一やさしいアドテク教室](https://www.cyberagent.co.jp/ir/personal/adtech/)：用語まとめもある．
* [SATORI, Ad Network（アドネットワーク）とは？を初心者にも分かりやすく解説します](https://satori.marketing/marketing-blog/ad-technology/ad-network/)：Ad Networkについて．
* [SATORI，Ad Exchange（アドエクスチェンジ）とは？を初心者にも分かりやすく解説します](https://satori.marketing/marketing-blog/ad-technology/ad-exchange/)：Ad Exchangeについて．
* [ウェブ部，【2017年6月更新】5分で完璧に理解できる！DSPの仕組みと新しい手法](【2017年6月更新】5分で完璧に理解できる！DSPの仕組みと新しい手法)：DSPについて．
* [Digital Marketing Lab，DMP（データマネジメントプラットフォーム）の仕組みと特徴](https://dmlab.jp/adtech/dmp.html)：DMPについて．
* [Qiita，広告と機械学習](http://qiita.com/fukkyy/items/b2d37b4797516d72225a)：2013年の記事だが，わかりやすい．
* [舘野啓，アドテクにおける機械学習技術](https://www.slideshare.net/ttpooh/tokyo-data-night-tokyodn)：数式がわかりやすい．
* [TechCrunch，Advertising Tech](https://techcrunch.com/advertising-tech/)：アドテク関連の最新ニュース．
