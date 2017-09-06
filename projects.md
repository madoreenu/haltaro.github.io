---
layout: page
title: Projects
permalink: /projects/
public: true
---

# 1. Network engineering

## 1.a [Comparing TCP algorithms](https://haltaro.github.io/comparing-tcp-algorithms) 

[ns-3](https://www.nsnam.org/)で12種類のTCP輻輳制御アルゴリズムをシミュレートし，[matplotlib](https://matplotlib.org/)で視覚化しました([Qiita](http://qiita.com/haltaro/items/d479538345357f08c595), [Github](https://github.com/haltaro/comparing-tcp-algorithms))．


![tcp.png]({{site.baseurl}}/images/comparing-tcp-algorithms.png)

# 2. Algorithmic trading

## 2.a [Animating alpha and beta](https://haltaro.github.io/animating-alpha-and-beta) 

[Pandas](http://pandas.pydata.org/)で世界株価時価総額トップ銘柄のアルファ値とベータ値を計算し，[matplotlib](https://matplotlib.org/)でアニメ化しました([Qiita](http://qiita.com/haltaro/items/e3e29264079f6b90d6df), [Github](https://github.com/haltaro/animating-alpha-and-beta))．


![ab.gif]({{site.baseurl}}/images/animating-alpha-and-beta.gif)

# 3. Machine learning

## 3.a [Predicting comic end](https://haltaro.github.io/predicting-comic-end) 

週刊少年ジャンプの掲載順から，短命作品を予測しました．掲載順のデータは[文化庁メディア芸術データベースのWeb API](https://mediaarts-db.bunka.go.jp/webapi_proto_documents.pdf)から取得し，予測には[TensorFlow](https://www.tensorflow.org/)で多層パーセプトロンを実装しました ([Qiita part1](http://qiita.com/haltaro/items/c54fa1855767f1a1abd5), [Qiita part2](http://qiita.com/haltaro/items/62d49875ed658ac8a93f), [Github](https://github.com/haltaro/predicting-comic-end))．下図は，短命作品と継続作品の相関関係の分析結果です．

![comic.png]({{site.baseurl}}/images/predicting-comic-end.png)

## 3.b [Deep learning in Japanese](https://haltaro.github.io/deep-learning-in-japanese)

Udacityの[Deep learning foundation nanodegree](https://www.udacity.com/course/deep-learning-nanodegree-foundation--nd101)の公開教材を和訳しています（[GitHub](https://github.com/haltaro/deep-learning-in-japanese)）．

![dlnd]({{site.baseurl}}/images/dlnd.png)

# 4. Deep learning foundations nanodegree

[Udacity](https://www.udacity.com/)で，[Deep learning foundations nanodegree](https://www.udacity.com/course/deep-learning-nanodegree-foundation--nd101) を修了しました．

## [Project 1 - First neural network](https://github.com/haltaro/udacity-deep-learning-project1/blob/master/DLND%20Your%20first%20neural%20network.ipynb)

フルスクラッチでニューラルネットワークを実装し，貸自転車のユーザ数を予測しました．下図は予測結果です．

![dlnd1.png]({{site.baseurl}}/images/dlnd1.png)

## [Project 2 - Image classification](https://github.com/haltaro/udacity-deep-learning-project2/blob/master/dlnd_image_classification.ipynb)

[TensorFlow](https://www.tensorflow.org/)でConvolutional neural networkを実装して，[CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html)の識別に挑戦しました．下図は予測結果です．

![dlnd2.png]({{site.baseurl}}/images/dlnd2.png)

## [Project 3 - Generate TV scripts](https://github.com/haltaro/udacity-deep-learning-project3/blob/master/dlnd_tv_script_generation.ipynb)

[TensorFlow](https://www.tensorflow.org/)でRecurrent neural networkを実装して，文章を自動生成しました．シンプソンズのスクリプトをもとに学習したモデルに，`homer_simpson`を入力すると，下記のようにそれらしい会話文が生成されました．

```
homer_simpson:(upset) marge, you're making a complete fool of yourse...(belches)
homer_simpson:(moans) i wanna take a nap so i'm awake for the meteor shower.
waylon_smithers: well...(to self) three beers, that's it.
homer_simpson:(to moe, slightly concerned) do you care about all this?
moe_szyslak:(to homer) hey, i don't need your sharity!(cries)
```

## [Project 4 - Translate a language](https://github.com/haltaro/udacity-deep-learning-project4/blob/master/dlnd_language_translation.ipynb)

[TensorFlow](https://www.tensorflow.org/)でSeq2Seqを実装し，機械翻訳に挑戦しました．下記のように英語をフランス語に変換できました[^1]．

```
Input
  Word Ids:      [33, 146, 10, 75, 91, 24, 16]
  English Words: ['he', 'saw', 'a', 'old', 'yellow', 'truck', '.']

Prediction
  Word Ids:      [188, 260, 34, 209, 248, 35, 234, 97, 1]
  French Words: il a vu un vieux camion jaune . <EOS>
```

[^1]: 正しい英語は`an old yellow truck`ですが，今回は`a`と`an`を学習するほどデータが無かったため，あえて`a old yellow truck`を入力しました．

## [Project 5 - Generate faces](https://github.com/haltaro/udacity-deep-learning-project5/blob/master/dlnd_face_generation.ipynb)

[TensorFlow](https://www.tensorflow.org/)でgenerative adversarial networkを実装し，顔画像の生成に挑戦しました．下図は，[celebA](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)データセットをもとに自動生成した顔画像です．

![celeba.gif]({{site.baseurl}}/images/celeba.gif)


