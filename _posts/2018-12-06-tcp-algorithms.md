---
layout: post
title: ns-3.27で使えるTCP輻輳制御アルゴリズム
updated: 2018-12-06
cover:  "/assets/2018-11-30-mist.jpg"
published: false
categories:
 - network
 - ns3
---

[Network engineering Advent Calendar 2018](https://qiita.com/advent-calendar/2018/network-engineering)の四日目の記事[^apology]．諸事情によりns-3.27でTCPの輻輳制御アルゴリズムを調査する必要があったので，調査結果をまとめておく．

[^apology]: 言い出しっぺの癖にめちゃくちゃ遅れてしまって申し訳ありません．

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

詳細は，[Floyd, Sally, Tom Henderson, and Andrei Gurtov. The NewReno modification to TCP's fast recovery algorithm. No. RFC 3782. 2004.](https://tools.ietf.org/html/rfc6582)を参照されたい．

## HighSpeed

大容量のチャネル向けに提案された輻輳制御アルゴリズム．このアルゴリズムは，Probe[^probing]時の$$cwnd$$の増加が大きく，また`recovery`フェイズにおける$$cwnd$$の回復が早い．このような特殊な動作は，$$cwnd$$が一定値より大きいときのみ実行されるため，輻輳時にHighSpeedはNewRenoとネットワークを共有した時に，帯域を一方的に専有することはない（このような性質をTCP friendlyと呼ぶ）．

[^probing]: $$cwnd=0$$のときにパケットロスが生じると，送信ノードも受信ノードも何も送信できなくなり，デッドロック状態になる．これを避けるため，送信ノードは一定間隔でペイロード長0のパケットを送ってACKを促す．これをWindow probeと呼ぶ

詳細は，[Floyd, Sally. HighSpeed TCP for large congestion windows. No. RFC 3649. 2003.](https://tools.ietf.org/html/rfc3649)を参照されたい．

## Westwood

Westwoodは，AIAD（Additive Increase/ Adaptive Decrease）方式を採用している．輻輳イベントが発生したとき，$$cwnd$$を半分にする代わりに，ネットワークの帯域を予測し，それをもとに$$cwnd$$を更新する．

詳細は，[Mascolo, Saverio, et al. "TCP westwood: Bandwidth estimation for enhanced transport over wireless links." Proceedings of the 7th annual international conference on Mobile computing and networking. ACM, 2001.](https://dl.acm.org/citation.cfm?id=381704)を参照されたい．

## Vegas

VegasはDelay-basedの輻輳制御アルゴリズムである．Vegasは継続的に取得したRTTから計算したスループットと，理想状態のスループットの差から，ボトルネックにスタックされているパケット量を推測する．輻輳を避けるため，上記のパケット量が$$\alpha$$と$$\beta$$の間になるよう$$cwnd$$を調整する．Slow startフェイズから，上記の$$cwnd$$調整フェイズに変更する閾値$$\gamma$$も，別途設定する必要がある．なお，Linuxにおける実装では，$$\alpha=2$$，$$\beta=4$$，$$\gamma=1$$が採用されている．

詳細は，[Brakmo, Lawrence S., and Larry L. Peterson. "TCP Vegas: End to end congestion avoidance on a global Internet." IEEE Journal on selected Areas in communications 13.8 (1995): 1465-1480.](https://ieeexplore.ieee.org/abstract/document/464716)を参照されたい．

## Scalable

Scalableは，大容量チャネルにおいて，より多くのデータを送信できるようNewRenoを改良した輻輳制御アルゴリズムである．輻輳イベントが検知しないとき，ACKを受信するたびに下式で$$cwnd$$を更新する．

$$ cwnd \leftarrow cwnd + 0.01 $$

輻輳イベントを検知したとき，Vegasは下式で$$cwnd$$を更新する．

$$ cwnd \leftarrow cwnd - \mathrm{ceil}\left(0.125 \cdot cwnd \right) $$

詳細は，[Kelly, Tom. "Scalable TCP: Improving performance in highspeed wide area networks." ACM SIGCOMM computer communication Review 33.2 (2003): 83-91.](https://dl.acm.org/citation.cfm?id=956989)を参照されたい．

## Veno

Venoは，無線通信におけるランダムなパケットロスに対応できるよう，NewRenoを改良した輻輳制御アルゴリズムである．ボトルネックにスタックされているパケット量（Backlogと呼ぶ）を推定し，輻輳しているか否かを判別する．

Backlog量$$N$$は下式で計算される．

$$ N = Actual \cdot (RTT - BaseRTT) $$

Venoは，$$N$$が閾値$$\beta$$より大きいか否かで，更新式を変更する．例えば，$$N$$が$$\beta$$より小さい時，

詳細は，[Fu, Cheng Peng, and Soung C. Liew. "TCP Veno: TCP enhancement for transmission over wireless access networks." IEEE Journal on selected areas in communications 21.2 (2003): 216-228.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.2.1469&rep=rep1&type=pdf)を参照されたい．

## Bic

詳細は，[Xu, Lisong, Khaled Harfoush, and Injong Rhee. "Binary increase congestion control (BIC) for fast long-distance networks." INFOCOM 2004. Twenty-third AnnualJoint Conference of the IEEE Computer and Communications Societies. Vol. 4. IEEE, 2004.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.91.1019&rep=rep1&type=pdf)を参照されたい．

## YeAH

詳細は，[Baiocchi, Andrea, Angelo P. Castellani, and Francesco Vacirca. "YeAH-TCP: yet another highspeed TCP." Proc. PFLDnet. Vol. 7. 2007.](https://www.researchgate.net/profile/Andrea_Baiocchi/publication/228561173_YeAH-TCP_Yet_another_highspeed_TCP/links/00b7d51ac57e095e39000000/YeAH-TCP-Yet-another-highspeed-TCP.pdf)を参照されたい．

## Illinois

詳細は，[Liu, Shao, Tamer Başar, and Ravi Srikant. "TCP-Illinois: A loss-and delay-based congestion control algorithm for high-speed networks." Performance Evaluation 65.6-7 (2008): 417-440.](http://tamerbasar.csl.illinois.edu/LiuBasarSrikantPerfEvalArtJun2008.pdf)を参照されたい．

## H-TCP

詳細は，[Leith, Douglas, and Robert Shorten. "H-TCP: TCP for high-speed and long-distance networks." Proceedings of PFLDnet. Vol. 2004. 2004.](https://www.scss.tcd.ie/Doug.Leith/pubs/htcp3.pdf)を参照されたい．

## LEDBAT

詳細は，[Shalunov, Sea, et al. Low extra delay background transport (LEDBAT). No. RFC 6817. 2012.](https://tools.ietf.org/html/rfc6817)を参照されたい．

# 感想

結構大変だったけど，勉強になった．誤りがあればご指摘いただきたい．
