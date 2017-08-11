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

* SQLのtypeとして，`text`，`integer`，`date`などがある．`text`および`date`は，`'2017-08-10'`のようにシングルクォートで囲む．
* 主なSQLのtypeは以下．
  * Text and string types:
    * `text`：長さに制限のない文字列．Pythonの`str`に相当．
    * `char(n)`：長さが`n`の文字列．
    * `varchar(n)`：長さが最大`n`の文字列．
  * Numeric types:
    * `integer`：整数型．Pythonの`int`に相当．
    * `real`：浮動小数点型．Pythonの`float`に相当．精度は小数第6位．
    * `double precision`：倍精度小数点．精度は小数第15位．
    * `decimal`：正確な小数型（？）．
  * Date and time types:
    * `date`：日付型．年，月，日．
    * `time`：時刻型．
    * `timestamp`：`date`および`time`．
* **select** *columns* **from** *tables* **where** *condition*; 構文．

# 3. Python DB-API

# 4. Deeper into SQL

# 5. Tournament Database


