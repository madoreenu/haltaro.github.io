---
layout: post
title: 作成中）Udacity, Introduction to relational databases受講メモ
updated: 2017-08-10 18:00 
categories:
 - data science
---

[Udacity, Introduction to relational databases](https://www.udacity.com/course/intro-to-relational-databases--ud197)の受講メモ．5部構成の無料講座．

# 1. Data and Tables

* Databaseは，同時に複数の人が編集可能．これが，普通のファイルと異なる点．
* Tableは，headerとbodyからなる．headerは，table nameと，column nameと，column typeからなる．bodyは，rowsとcolumnsからなる．
* 複数の行に跨る演算をaggregationと呼ぶ．SQLで使えるaggregationの代表的なものとして，count，avg，max，min，sumなどがある．
* codeからdatabaseに`query`を出すと，`result`を返される．`result`は，原則的にTable形式．
* Database中でデータの唯一性を担保するために，idを与えることがある．このように識別に用いられるcolumnを`primary key`と呼ぶ．
* 複数の情報を持つオブジェクトを定義するよりは，複数のTableで管理したほうが効率的．

# 2. Elements of SQL

# 3. Python DB-API

# 4. Deeper into SQL

# 5. Tournament Database


