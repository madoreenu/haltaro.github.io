---
layout: post
title: 作成中）Udacity, Intro to Hadoop and MapReduce受講メモ
updated: 2017-08-12 16:00 
categories:
 - data science
---

[Udacity, Intro to Hadoop and MapReduce](https://www.udacity.com/course/intro-to-hadoop-and-mapreduce--ud617)の受講メモ．6部構成の無料講座．

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


# 2. HDFS and MapReduce

* HDFSでは，データを64Mbyteの**ブロック**に分割し，それぞれ別のマシンに保存する．
* **ネームノード**は，どのブロックがどのマシンに保存されているかという**メタデータ**を管理する．
* 冗長性のため，Hadoopはブロックを三回複製する．またネームノードの複製も用意する．
* `hadoop fs -ls`などで，HDFSにアクセスできる．`-ls`の部分は，UNIXのファイルシステムコマンドを利用可能．
* ハッシュテーブルは，Big Data適用時に，処理時間とメモリ消費という課題があった．
* MapReduceのまとめ：
    * **Map**：小さく分割されたデータを，`<key, value>`形式で保存し，同一`key`でまとめる．Mapperの出力を中間レコード（Intermediate records）と呼ぶ．
    * **Shuffle and sort**：中間レコードをReduceに渡し，`key`でソートする．
    * **Reduce**：`key`毎に処理し，`<key, values>`リストを作成する．
* 最終結果をソートするためには，単独のReducerを使うか，別途処理を行うか．
* 各Reducerが受け取る`key`の数は，事前にはわからない．等分されるとは限らない．
* **Job tracker**が，MapperとReducerにジョブを割り当てる．
* 各デーモンは，**Task tracker**を持つ．
* HadoopではJavaが使われるが，Pythonを使うこともできる．
* `hs {mapper script} {reducer script} {input_file} {output directory}`で実行できる．ただし，`{output directory}`が既に存在する場合，エラーが返されるので注意．
* `hadoop fs -put`でデータをHDFSに保存し，`hadoop fs -get`で取り出す．
* 仮想マシンで実際にHadoopを動かす．以下，参考：
    * [インストールと初期設定](https://docs.google.com/document/d/1v0zGBZ6EHap-Smsr3x3sGGpDW-54m82kDpPKC2M6uiY/pub)
    * [ファイル共有](https://docs.google.com/document/d/1MZ_rNxJhR4HCU1qJ2-w7xlk2MTHVqa9lnl_uj-zRkzk/pub)

<iframe width="100%" height="480" src="https://www.youtube.com/embed/l0I_2nyPNZM?rel=0" frameborder="0" allowfullscreen></iframe>

<iframe width="100%" height="480" src="https://www.youtube.com/embed/d5TZ_2I7dwE?rel=0" frameborder="0" allowfullscreen></iframe>

* 技術的な詳細は，[Chapter 6 of Tom White’s essential text, Hadoop: The Definitive Guide](http://go.cloudera.com/udacity-lesson-2)を参照．

# 3. MapReduce Code

# 4. Project

# 5. MapReduce Design Patterns

# 6. Project Prep
