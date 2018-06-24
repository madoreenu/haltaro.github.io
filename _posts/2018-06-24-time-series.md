---
layout: post
title: 萩原淳一郎，基礎からわかる時系列分析
updated: 2018-06-24
cover:  "/assets/2018-06-24-berries.jpg"
categories:
 - statistics
---

[萩原淳一郎，基礎からわかる時系列分析 ―Rで実践するカルマンフィルタ・MCMC・粒子フィルター](http://amzn.asia/bTrcjv0)をざっと読んで状態空間モデルを勉強した．線形・ガウス型の状態空間モデルの場合はカルマンフィルタで解析的に解けるが，一般状態空間モデルの場合は，フィルタリング分布・予測分布・平滑化分布の積分計算を必ずしも解析的に解けない．そこで，MCMCを用いた一括解法や，粒子フィルタによる逐次解法が提案されている．

# 確率・統計に関する基礎

- 周辺化消去は，同時分布から外したい変数の影響を，あらかじめ平均的に考慮することに相当する．なるほど，腑に落ちた．
- 定常過程と非定常過程．
    - 強定常：確率過程の確率分布が時点$$t$$によらず一定．
    - 弱定常：確率過程の平均・分散・自己共分散・自己相関係数が時点$$t$$によらず一定．

# 時系列分析ひとめぐり

- 五数要約：最小値・25%値・中央値・75%値・最大値．Rだと`summary()`で，Python（pandas）だと`DataFrame.describe()`で確認できる．
- 自己相関係数．$$\frac{\mathrm{Cov}[X_{t}, X_{t-k} ]}{\sqrt{\mathrm{Var}[X_t]}\sqrt{\mathrm{Var}[X_{t-k}]}}$$．
- 時系列データの成分分解：レベル＋傾き＋周期．
- ホルト・ウィンタース法．指数加重型移動平均（EWMA：Exponentially Weighted Moving Average）の一種．Rでは，`HoltWinters()`関数で実施できる．
- 残差を確認して，モデルの妥当性を分析する．残差の自己相関により，周期性を上手く捉えられたか確認できる．
- 状態空間モデルの解法の分類：
    - 線形・ガウス型状態空間モデル：
        - 一括型解法：ウィナーフィルタ．
        - 逐次型解法：カルマンフィルタ．
    - 一般状態空間モデル：
        - 一括型解法：MCMCを利用した解法．
        - 逐次型解法：粒子フィルタ．

# 状態空間モデル

- 方程式による表現：
    - 状態方程式[^state]：$$\mathbf{x}_t = f ( \mathbf{x}_{t-1}, \mathbf{w}_{t-1}) $$
    - 観測方程式：$$y_t = h ( \mathbf{x}_{t}, v_{t}) $$
- 確率分布による表現：
    - 状態方程式に相当：$$p(\mathbf{x}_t \mid \mathbf{x}_{0:t-1}, y_{0:t-1}) = p(\mathbf{x}_t \mid \mathbf{x}_{t-1}) $$
    - 観測方程式に相当：$$p(y_t \mid \mathbf{x}_{0:t}, y_{0:t-1}) = p(y_t\mid \mathbf{x}_{t}) $$
- 状態空間モデルの同時分布：$$p(\mathbf{x}_{0:T}, y_{0:T}) = p(\mathbf{x}_0) \prod_{t=1}^{T} p(y_t\mid \mathbf{x}_{t}) p(\mathbf{x}_t \mid \mathbf{x}_{t-1})$$
- ARIMAモデルと状態空間モデルは密接な関係がある．

# 状態空間モデルにおける状態の推定

- 状態の周辺事後分布：$$p(\mathbf{x}_{t'} \mid y_{1:t}) = \int p(\mathbf{x}_{0}, \mathbf{x}_{1}, \dots \mathbf{x}_{t'}, \dots \mid y_{1:t}) d\mathbf{x}_{t'以外}$$
    - $$t' < t$$：平滑化分布
    - $$t' = t$$：フィルタリング分布
    - $$t' > t$$：予測分布
- フィルタリング分布：$$p(\mathbf{x}_{t} \mid y_{1:t}) = p(\mathbf{x}_{t} \mid y_{1:t-1}) \frac{p(y_{t} \mid \mathbf{x}_{t})}{p(y_{t}) \mid p(y_{1:t-1})} $$
    - モデルの状態方程式$$p(y_{t} \mid \mathbf{x}_{t})$$と，以下の一期先予測分布，一期先予測尤度からなる．
    - 一期先予測分布： $$p(\mathbf{x}_{t} \mid y_{1:t-1}) = \int p(\mathbf{x}_{t} \mid \mathbf{x}_{t-1}) p(\mathbf{x}_{t} \mid y_{1:t-1}) d\mathbf{x}_{t-1} $$
    - 一期先予測尤度[^likelihood]：$$p(y_{t} \mid y_{1:t-1}) = \int p(y_t \mid \mathbf{x}_{t} ) p(\mathbf{x}_{t} \mid y_{1:t-1}) d\mathbf{x}_{t-1} $$
- 予測分布：
    - 定式化：$$p(\mathbf{x}_{t+k} \mid y_{1:t}) = \int p(\mathbf{x}_{t+k} \mid \mathbf{x}_{t+k-1}) p(\mathbf{x}_{t+k-1} \mid y_{1:t}) d\mathbf{x}_{t+k-1} $$
    - 一期先予測分布をもとに，状態方程式に基いて時間順方向への遷移を$$k-1$$解繰り返したもの．
- 平滑化分布：
    - 定式化：$$p(\mathbf{x}_{t} \mid y_{1:T}) = p(\mathbf{x}_{t} \mid y_{1:t}) \int \frac{p(\mathbf{x}_{t+1} \mid \mathbf{x}_{t})}{p(\mathbf{x}_{t+1} \mid y_{1:t})} p(\mathbf{x}_{t+1} \mid y_{1:T}) d \mathbf{x}_{t+1}$$
    - p(\mathbf{x}_{t} \mid y_{1:t})はフィルタリング分布，p(\mathbf{x}_{t+1} \mid \mathbf{x}_{t})は状態方程式，p(\mathbf{x}_{t+1} \mid y_{1:t})は予測分布，p(\mathbf{x}_{t+1} \mid y_{1:T}) は1時点先の平滑化分布．
    - 平滑化分布は，フィルタリング分布を再帰的に補正したもの．
- パラメータ集合を$$\mathbf{\theta}$$とすると，対数尤度は$$l(\mathbf{\theta}) = \sum_{t=1}^{T} \mathrm{log} p( y_t \mid y_{1:t-1} ; \mathbf{\theta})$$．
    - 一期先予測尤度が含まれているため，特定のデータに基づきながら，過去の情報のみから見洗の値を当てる際の予測能力を踏まえた指標になっている．
    - この式には状態が登場しないため，周辺尤度あるいは対数周辺尤度と呼ばれることがある．
- 状態空間モデルにおけるパラメータの扱い．
    - $$\mathbf{\theta}$$が確率変数でない：$$\mathrm{argmax}_{\mathbf{\theta}} l(\mathbf{\theta})$$を準ニュートン法やEMアルゴリズムで求める．
    - $$\mathbf{\theta}$$が確率変数：$$\mathrm{argmax}_{\mathbf{\theta}} p(\mathbf{\theta} \mid y_{1:t}) \propto \mathrm{argmax}_{\mathbf{\theta}} \{ p(y_{1:t} \mid \mathbf{\theta} ) +  p(\mathbf{\theta} ) \}$$をMAP推定で求める．
- パラメータを確率変数として扱う場合は，たとえもともと線形ガウス型の状態空間モデルであっても，一般状態空間モデルになる．つまり，ウィナーフィルタやカルマンフィルタでは直接解を求められない．

# 線形・ガウス型状態空間モデルの一括解法

# 線形・ガウス型状態空間モデルの逐次解法

# 一般状態空間モデルの一括解法

- フィルタリング分布，予測分布，および平滑化分布には多次元の積分計算が含まれる．線形・ガウス型状態空間モデルの場合は，**幸運にも** 解析的に解けたが，一般状態空間モデルの場合は必ずしも解析的に解けないため，工夫が必要：
  - グリッドフィルタ：数値積分を活用するアプローチ．
  - 重点サンプリング：ラプラス近似を利用して，一般状態空間モデルにおける分布を線形・ガウス型状態空間モデルにおける分布で近似するアプローチ．
  - MCMC（マルコフ連鎖モンテカルロ法；Markov chain Monte Carlo）：求めたい分布からのサンプルを直接生成するアプローチ．

# 一般状態空間モデルの逐次解法

[^state]: システム方程式とも呼ばれる．

[^likelihood]: なぜ尤度と呼ぶんだろう．まだ腑に落ちてない．