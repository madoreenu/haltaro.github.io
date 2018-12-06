---
layout: post
title: ns-3.27で使えるTCP輻輳制御アルゴリズム
updated: 2018-12-06
cover:  "/assets/2018-11-30-mist.jpg"
published: false
categories:
 - network
---

[Network engineering Advent Calendar 2018](https://qiita.com/advent-calendar/2018/network-engineering)の四日目の記事．諸事情によりns-3.27でTCPの輻輳制御アルゴリズムを調査する必要があったので，調査結果をまとめておく．

もしご興味のある方は，以下の記事を参考に実験すると楽しいかもしれない．

- 環境構築：[VirtualBox+Vagrantでns-3.27環境を構築する - Memotaro](https://haltaro.github.io/2018/11/30/ns3-vagrant#undefined)
- 比較実験（ns-3.26）：[ns-3でTCPの輻輳制御を観察する - Memotaro](https://haltaro.github.io/2018/07/13/tcp-ns3#ns-3-network-simulator-3)

# 前提知識

## ns-3

[ns-3](https://www.nsnam.org/)は，オープンソースの離散事象ネットワークシミュレータ．前職ではこれを使って独自のプロトコルを実装し，実験結果を論文化する仕事をしていた．基本的にLinux上でしか動かず，また環境構築がやや煩雑なので，一般ユーザにとっては敷居が高い[^me]．環境構築については，[VirtualBox+Vagrantでns-3.27環境を構築する - Memotaro](https://haltaro.github.io/2018/11/30/ns3-vagrant#undefined)を，ns-3で何ができるかについては，[ns-3でTCPの輻輳制御を観察する - Memotaro](https://haltaro.github.io/2018/07/13/tcp-ns3)を参照されたい．

[^me]: 少なくとも私はそうだった．

## TCP

TCP（Transmission Control Protocol）は，OSI参照モデルのトランスポート層（つまり，IPの一つ上の層）に該当するプロトコル．同じくトランスポート層のプロトコルであるUDP（User Datagram Protocol）と比較されることが多い．ざっくり言うと，TCPは通信の信頼性を重視しているのに対し，UDPは高速性やリアルタイム性を重視している．例えば，動画のストリーミングではUDPを利用することが多いが，動画のダウンロードではTCPを利用することが多い．インターネット全体における割合で言うと，TCPを使った通信の方が圧倒的に多い．

TCPの特徴の一つは，輻輳制御である．輻輳とは，コンピュータネットワークにおける渋滞を表す．輻輳時は，ルータやハブでバッファ溢れが発生し，ネットワーク中のパケットが廃棄されてしまう．当該パケットの送受信ノードが大きな損失を被るのは言うまでもないが，他のノードも従来どおりネットワークを利用できなくなる場合があるため，輻輳が起きないよう制御する必要がある．TCPの輻輳制御では，下式で送信データ量を調整する．

$$swnd = \mathrm{min}(cwnd, rwnd) - acked$$

ここで，$$swnd$$は送信データ量，$$cwnd$$は送信ノードが内部で保持する変数である輻輳窓（Congestion window），$$rwnd$$は受信ノードから告知された受信窓（Receive window），$$acked$$は確認応答を受信したデータ量を表す．単位はバイトである[^unit]．受信ノードの最大受信量$$rwnd$$と，受信ノードに到着したデータ量を表す$$acked$$は，送信ノード側で制御できない所与の値である．つまり，TCPの送信ノードは，ネットワークの混み具合に応じて輻輳窓$$cwnd$$を調整することで，輻輳制御を行う．これまで，非常に多くの輻輳制御アルゴリズムが提案されてきた．その全てを網羅することはできないので，ns-3.27で実装されている主要なものにしぼり，その特徴をまとめる．

![model.png](https://qiita-image-store.s3.amazonaws.com/0/151195/ea523d49-c229-2d46-a3c5-7290b3f82dff.png)

[^unit]: TCPの輻輳制御アルゴリズムでは，単位としてセグメントを使うときとバイトを使うときがあり，混乱しないよう注意が必要．間違うのは私だけかもしれないが．

## 輻輳制御アルゴリズム

輻輳制御アルゴリズムとは，TCPにおける$$cwnd$$の更新規則をまとめたアルゴリズムである．基本的なアイデアとしては，TCPの受信ノードから返ってくる確認応答（ACK：Acknowledgement）をもとに，往復時間（RTT：Round Trip Time）やパケットロスを計測し，これをもとに推定したネットワークの混み具合に応じて，$$cwnd$$を更新する．

# アルゴリズム一覧

[Congestion Control Algorithms - ns-3](https://www.nsnam.org/docs/models/html/tcp.html#congestion-control-algorithms)を参考に，ns-3.27で使用可能な輻輳制御アルゴリズムをまとめた．

[^future]: 時間ができたら，独自のTCPアルゴリズムを実装する方法もまとめておきたい．いつになるかわからないが．

- [NewReno](https://haltaro.github.io/2018/12/06/tcp-algorithms#newreno)
- [HighSpeed](https://haltaro.github.io/2018/12/06/tcp-algorithms#highspeed)
- [Westwood](https://haltaro.github.io/2018/12/06/tcp-algorithms#westwood)
- [Vegas](https://haltaro.github.io/2018/12/06/tcp-algorithms#vegas)
- [Scalable](https://haltaro.github.io/2018/12/06/tcp-algorithms#scalable)
- [Veno](https://haltaro.github.io/2018/12/06/tcp-algorithms#veno)
- [Bic](https://haltaro.github.io/2018/12/06/tcp-algorithms#bic)
- [YeAH](https://haltaro.github.io/2018/12/06/tcp-algorithms#yeah)
- [Illinois](https://haltaro.github.io/2018/12/06/tcp-algorithms#illinois)
- [H-TCP](https://haltaro.github.io/2018/12/06/tcp-algorithms#h-tcp)
- [LEDBAT](https://haltaro.github.io/2018/12/06/tcp-algorithms#ledbat)

ここでは，ns-3.27でデフォルト実装されているものに絞っているが，`ns-3.27/src/internet/model`にソースコードを格納すれば，自由にアルゴリズムを追加可能である[^future]．例えば，Linux2.6.19以降で標準搭載されている[CUBIC](http://www4.ncsu.edu/~rhee/export/bitcp/cubic-paper.pdf)は，[こちら](http://web.cs.wpi.edu/~claypool/papers/tcp-cubic/)からソースコードを入手できる．

なお，ほとんどのアルゴリズムでパケットロス時やタイムアウト時の動作は共通しているため，本記事では通常状態（パケットロスやタイムアウトがない状態）における動作の違いに焦点をあてる．

## NewReno

最もメジャーなアルゴリズムの一つ．$$cwnd$$が$$ssthresh$$より小さい場合はSlow startフェイズ，大きい場合はCongestion avoidanceフェイズに移り，それぞれ以下の更新式を用いる．

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

ここで，上式は**ACKを受信するたび**に更新されることに注意されたい．また，上式の単位はセグメントである．Slow startフェイズ（二行目）においては，ACKを受信するたびに$$cwnd$$が一つずつ増加し，その結果受信することになるACKも一つ増えるため，$$cwnd$$は指数的に増加する．一方でCongestion avoidanceフェイズ（三行目）においては，$$cwnd$$は線形に増加する．

詳細は，[T. Henderson, et al., "The NewReno Modification to TCP’s Fast Recovery Algorithm," Request for Comments: 6582, 2012.](https://tools.ietf.org/html/rfc6582)を参照されたい．

## HighSpeed

大容量のチャネル向けに提案された輻輳制御アルゴリズム．

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

詳細は，[S. Floyd, et al., "HighSpeed TCP for Large Congestion Windows," Request for Comments: 3649, 2003](https://tools.ietf.org/html/rfc3649)を参照されたい．

## Westwood

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## Vegas

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## Scalable

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## Veno

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## Bic

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## YeAH

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## Illinois

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## H-TCP

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

## LEDBAT

$$
\begin{align}
&\mathbf{If}~ cwnd \leq ssthresh\\
&~~~~\mathbf{then}~ cwnd \leftarrow cwnd + 1 \\
&~~~~\mathbf{else}~ cwnd \leftarrow cwnd + \frac{1}{cwnd}
\end{align}
$$

# 感想

結構大変だったけど，勉強になった．誤りがあればご指摘いただきたい．
