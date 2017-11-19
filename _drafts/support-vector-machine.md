---
layout: post
title: Support vector machineまとめ
updated: 2017-10-25 22:00
categories:
 - machine learning
---

本記事では，[栗田多喜夫，サポートベクターマシン入門](http://home.hiroshima-u.ac.jp/tkurita/lecture/svm.pdf)や[C. M. ビショップ，パターン認識と機械学習](http://amzn.asia/0OTDQtT)を参考に，
[Support vector machine](https://ja.wikipedia.org/wiki/%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%83%99%E3%82%AF%E3%82%BF%E3%83%BC%E3%83%9E%E3%82%B7%E3%83%B3)（SVM）の基本をまとめる．
SVMは，現在知られている手法の中でも認識性能が優れたモデルの一つであり，分類および回帰の両方に適用可能である．

最も単純な**ハードマージン線形SVM**から，**ソフトマージン線形SVM**，そしてカーネルトリックを使った**非線形SVM**と，徐々に複雑なモデルを解説します．

# 1. 記号類

* $$\mathbf{x}_n$$：$$n$$番目データの特徴ベクトル．
* $$y_n$$：$$n$$番目データの教師ラベル．$$y_n \in \{-1, 1\}$$．
* $$\mathbf{w}$$，$$b$$：ラベルを予測するためのパラメータ．
* $$\hat{y}(\mathbf{x}_n)$$：$$n$$番目のデータ$$\mathbf{x}_n$$に対するラベルの予測結果．$$\hat{y}(\mathbf{x}_n) > 0$$のときラベルを$$y_n=1$$と予測し，それ以外のときはラベルを$$y_n=-1$$と予測する．
* $$\xi$$：ソフトマージンSVMで用いるパラメータ．
* $$\mathbf{\phi}(\mathbf{x}_n)$$：$$n$$番目のデータの特徴ベクトル$$\mathbf{x}_n$$の写像後のベクトル．$$\mathbf{x}_n$$と$$\mathbf{\phi}(\mathbf{x}_n)$$の次元は必ずしも同じである必要はない．


# 2. ハードマージン線形SVM

$$
\begin{align*}
\hat{y} \left( \mathbf{x} \right) = \mathbf{w}^{T} \mathbf{\phi}(\mathbf{x}) + b \tag{1}
\end{align*}
$$

# 3. ソフトマージン線形SVM

# 4. 非線形SVM

# 5. 感想

# 参考

* [栗田多喜夫，サポートベクターマシン入門](http://home.hiroshima-u.ac.jp/tkurita/lecture/svm.pdf)
* [C.M.ビショップ，パターン認識と機械学習 下](http://amzn.asia/0OTDQtT)
