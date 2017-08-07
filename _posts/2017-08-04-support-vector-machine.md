---
layout: post
title: 作成中）Support vector machineの理論と実装
updated: 2017-08-04 22:00 
categories:
 - machine learning
---

[パターン認識と機械学習](https://www.amazon.co.jp/%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E8%AA%8D%E8%AD%98%E3%81%A8%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92-%E4%B8%8B-%E3%83%99%E3%82%A4%E3%82%BA%E7%90%86%E8%AB%96%E3%81%AB%E3%82%88%E3%82%8B%E7%B5%B1%E8%A8%88%E7%9A%84%E4%BA%88%E6%B8%AC-C-M-%E3%83%93%E3%82%B7%E3%83%A7%E3%83%83%E3%83%97/dp/4621061240/ref=pd_sim_14_1?_encoding=UTF8&psc=1&refRID=75MTQH13HRTSXQWGQARY)でsupport vector machine（SVM）について復習した．SVMは疎な解を持つ識別関数の一種であり，クラス分類や回帰など，様々な応用が可能．モデル学習が二次計画問題に帰着するため，局所解=最適解という扱いやすい性質を持つ．

# 1. 理論

## 1.a コンセプト

## 1.b 最大マージン分類器

$$
\begin{align*} 
y \left( \mathbf{x} \right) = \mathbf{w}^{T} \mathbf{\phi}(\mathbf{x}) + b \tag{1}
\end{align*}
$$

## 1.c ラグランジュ乗数法

## 1.d カーネルトリック

# 2. 実装

学習目的であれば，ソルバで二次計画法を解いても良さそう．実務目的であれば，無難にライブラリを使ったほうが良さそう．

## 2.a ソルバで二次計画法を解く

Pythonの二次計画法ライブラリとしては，[CVXOPT](http://cvxopt.org/)が人気．

## 2.b ライブラリで実装

[scikit-learn](http://scikit-learn.org/stable/index.html)の[`sklearn.svm`](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.svm)モジュールはとても便利．

# 3. 実験

# 参考文献

* [C.M.ビショップ，パターン認識と機械学習 下](https://www.amazon.co.jp/%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E8%AA%8D%E8%AD%98%E3%81%A8%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92-%E4%B8%8B-%E3%83%99%E3%82%A4%E3%82%BA%E7%90%86%E8%AB%96%E3%81%AB%E3%82%88%E3%82%8B%E7%B5%B1%E8%A8%88%E7%9A%84%E4%BA%88%E6%B8%AC-C-M-%E3%83%93%E3%82%B7%E3%83%A7%E3%83%83%E3%83%97/dp/4621061240/ref=pd_lpo_sbs_14_img_2?_encoding=UTF8&psc=1&refRID=2J0S7A4J37ASEZ0JMGQW)：SVMが登場するのは下巻．ただし，ラグランジュ乗数法の詳細は上巻の付録にある．
* [`sklearn.svm`: Support Vector Machines](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.svm)：便利すぎるSVMモジュール．
