---
layout: post
title: 機械学習関連で今後やりたいこと 
updated: 2017-08-02 22:00 
categories:
 - machine learning 
---


[Udacity](https://www.udacity.com/)の[Deep learning foundations nanodegree]()を修了して，基本はある程度押さえられたし，論文も読めるようになった．次にやりたいことをリストアップしておく．

# a. 本業に活かす

可能ならば，というレベル．技術ありきで問題を後付けするのは悪い癖なので，機械学習に執着せず，フラットに他の技術と比較するよう注意したい．

# b. 新プロジェクトを立ち上げる

## b.1 顔画像から実子判定

数年前，DNA鑑定が大流行したので，ニーズはありそう．実子であれば，両親の面影が顔に顕れるはずだし，この類のタスクはdeep learningの得意技の気がする．

下記のキーワードで，盛んに研究が行われている．

* `kinship identification`
* `kinship verification`
* `kinship recognition`

また，非商用の研究用途に限れば，データセットは入手可能である．

* [UB KinFace Database](http://www1.ece.neu.edu/~yunfu/research/Kinface/Kinface.htm)

問題は２つある．
* **実生活に波風が立つ**：なまじ新婚なので，不穏な空気になる．他意はないのに．
* **道徳的にアレ**：センシティブな話題なので，慎重になったほうが良い．研究用途で画像セットを使うぶんには問題ない？

リスクが大きすぎるので，とりあえずやめておこう．

## b.2 君の名はの三葉の中身を顔画像から推定

最近DVDが出たので．本作は作画の完成度が高いので，たぶんうまくいくと思う．組紐の有無とか眉毛の角度とかを学習してくれたら面白い．ちなみに，アニメの顔検出は[OpenCV](http://opencv.org/)で自動化できるので，そこまで大変じゃない．

* [OpenCVによるアニメ顔検出ならlbpcascade_animeface.xml](http://ultraist.hatenablog.com/entry/20110718/1310965532)

## b.3 スラムダンクの赤木と高砂を顔画像から推定

大好きなので．「桜木がAIなら湘北が勝ってた」あるいは「AIでも見間違うから桜木のミスはしょうがない」と，結果がどちらに転んでもオイシイ．問題は，画像データの収集と，ラベル数の偏り．

## b.4 カイジの限定ジャンケンを強化学習

[限定ジャンケン](https://ja.wikipedia.org/wiki/%E8%B3%AD%E5%8D%9A%E9%BB%99%E7%A4%BA%E9%8C%B2%E3%82%AB%E3%82%A4%E3%82%B8#.E9.99.90.E5.AE.9A.E3.82.B8.E3.83.A3.E3.83.B3.E3.82.B1.E3.83.B3)は，大学入試の二次試験で出てもおかしくないくらい，面白い問題だと思う[^kaiji]．さすがに，カードの買い占めや星の売買を考慮すると問題が複雑になりすぎる[^2]ので，「全体の手数の総数を見て，次の自分の手を決定する問題」程度に単純化すれば，実装できそうな気がする．

[^1]: 1992年の東大入試では，じゃんけんグリコに関する問題が出されたみたい．[じゃんけんグリコの最適戦略と東大の問題](http://mathtrain.jp/grk)
[^2]: 限定ジャンケンの本質はそこな気がするので，残念だけど．

# c. 地道に学習をすすめる

## c.1 Deep learning foundations nanodegreeの和訳

[こちら](https://haltaro.github.io/deep-learning-in-japanese/)で地道に進めている．翻訳するためには，原文を完全に理解しないといけないので，とても勉強になる．

## c.2 Fast.ai

巷で評判の良い，[fast.ai](http://www.fast.ai/)のMOOCを受講する．

* [Part 1 - Practical Deep Learning For Coders](http://course.fast.ai/)
* [Part 2 - Cutting Edge Deep Learning For Coders](http://course.fast.ai/part2.html)

Part 1では，Kaggleの[犬猫分類コンペ](https://www.kaggle.com/c/dogs-vs-cats)で上位に食い込むためのテクニックを教えてくれるらしい．

## c.3 Kaggle

結局，実データで修行するのが一番良い気がする．以下のコンペは本業とも関連するので，トライしてみたい．

* [Web Traffic Time Series Forecasting](https://www.kaggle.com/c/web-traffic-time-series-forecasting)
