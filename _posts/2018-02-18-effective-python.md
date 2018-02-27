---
layout: post
title: Brett Slatkin，Effective Python
updated: 2018-02-18 13:00
cover: "/assets/2018-02-17-effective-python.jpg"
categories:
 - python
---

<i class="fa fa-spinner"></i> **更新中**：[Brett Slatkin，Effective Python ―Pythonプログラムを改良する59項目](http://amzn.asia/gDvdj6b)を読む．[Python](https://www.python.org/)を効率的に書くための59のヒントが紹介されている．

特に心に残った項目を以下にまとめる．Jupyter notebookは[こちら](https://github.com/haltaro/effective-python)．

# 1章．Pythonic thinking

## リスト内包表記には，3つ以上の式を避ける

<script src="https://gist.github.com/haltaro/64f7a37df260ad506cb9be4d7b0ad106.js"></script>

リスト内包表記に毒されすぎて，もとの表記の何がわかりづらいのか，また修正された表記でわかりやすくなったのかピンとこない．気をつけないと．

## 大きな内包表記にはジェネレータ式を考える

<script src="https://gist.github.com/haltaro/9284d0b7762c8d24b0cabf09af1723ef.js"></script>

イテレータとジェネレータについては，[Pythonのイテレータとジェネレータ - Qiita](https://qiita.com/tomotaka_ito/items/35f3eb108f587022fa09)がわかりやすい．

## `try`/`except`/`else`/`finally`の各ブロックを活用する

- `except`：エラーが補足された場合の処理．
- `else`：エラーが捕捉されなかった場合の処理．
- `finally`：エラーの捕捉にかかわらず，最後に実行される処理．

# 2章．関数

## `None`を返すよりは例外を選ぶ

<script src="https://gist.github.com/haltaro/7444e23cfc581fb1f2cb5dc8c8744503.js"></script>

`None`と，`0`や空白文字などの他の値がすべて条件式において`False`と評価されるため，エラーを引き起こしやすい．それはそうと，`raise from`構文がよくわからない．あとで確認しよう．

## クロージャが変数スコープとどう関わるか知っておく
