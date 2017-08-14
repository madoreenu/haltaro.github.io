---
layout: post
title: 作成中）Udacity, Intro to Hadoop and MapReduce受講メモ
updated: 2017-08-12 16:00 
categories:
 - data science
---

[Udacity, Intro to Hadoop and MapReduce](https://www.udacity.com/course/intro-to-hadoop-and-mapreduce--ud617)の受講メモ．8部構成の無料講座．

<iframe width="100%" height="480" src="https://www.youtube.com/embed/DEQNknALf_8?rel=0" frameborder="0" allowfullscreen></iframe>

# 1. Big Data

* Big Dataとは，一つのマシンでは処理しきれないほど大量のデータである．
* Big Dataにおける課題は主に以下の２つ：
    * データが高速に生成されること．
    * データが異なるソースから多様なフォーマットで生成されること．
* データの性質を表現する三つのV：
    * **Volume**（量）：データを保存するだけではなく，処理することも考える必要がある．
    * **Variety**（多様性）：非構造データや半構造データが増加しており，従来のデータベースへは保管が難しい．もし非構造データをそのまま保存できれば，後で活用できるかもしれない．`Hadoop`では，データフォーマットによらず，そのまま保存できる．
    * **Velocity**（速度）：処理速度が速ければ速いほど，より多くのビジネスチャンスが生まれる．
* Hadoopの由来は，製作者の子供のおもちゃ．
* Hadoopの技術的コアは２つ：
    * **HDFS**（Hadoop distributed file system）による分散ファイル保存．
    * **MapReduce**によるデータ処理．
* Hadoopでは，データの保存及び処理が，クラスタ毎に行われる．
* Hadoop ecosystem：
    * **Pig**，**Hive**：MapReduceのハイレベルインターフェース．SQLチックに使える．
    * **Impala**：HDFSへの低レベルインターフェース．PigやHiveより高速．
    * **Sqoop**，**Flume**：他のデータベース上のデータを，クラスタとして保存できる．
    * **HBase**：HDFS上のリアルタイムデータベース．
    * **Hue**：GUI．
    * **Oozie**：ワークフロー管理ツール．
    * **Mahout**：機械学習ライブラリ．
    * **Cloudera**：環境構築ツール．上記のソフトウェアをまとめてインストールできる．

# 2. Problem Set

# 3. HDFS and MapReduce

# 4. Problem Set

# 5. MapReduce Code

# 6. Project

# 7. MapReduce Design Patterns

# 8. Project Prep
