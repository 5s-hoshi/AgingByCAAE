# AgingByCAAE


## 参考
### Age progression/Regression by Conditional Adversarial Autoencoder
https://arxiv.org/pdf/1702.08423.pdf

### Abstract
大量の顔写真データを用いて、特定の顔写真の老化・若返りを行う試み。<br>
CAAE:畳込みエンコーダで潜在的ベクトルに顔の特徴をマッピング→畳込み解消器により年齢を条件とした顔を表す多様体に射影する。

### Intro
個性を維持したまま年齢を変化させるのが難しい。データに対する制約が多いと不便。加齢の方が進んでいるらしい。<br>
いま、多様体上の一点と顔写真を対応付ける。年齢とともに多様体上を移動する。多様体上の年齢を表す曲面を探しているのか？<br>
多様体の学習のためにCAAEを用いる。高次元多様体上での操作は大変だから畳込みエンコーダを用いて次元を落とす。そののち畳込み解消器で射影する。
その両者にGANがある。メリットは以下の4つ:<br>
・写真のようにリアルで、若返りと老化の同時実現<br>
・学習データにペアのサンプルを必要としない<br>
・年齢と個性を分離することでゴーストの発生を防ぎつつ個性を保つ<br>
・ポーズ、表情、環境に対し頑健<br>
<br>
![D:\mathbb{R}^n \rightarrow \{0,1\}](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Ctextstyle+D%3A%5Cmathbb%7BR%7D%5En+%5Crightarrow+%5C%7B0%2C1%5C%7D)
(これは嘘かも),
![G:[0,1] \rightarrow \mathbb{R}^n](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Ctextstyle+G%3A%5B0%2C1%5D+%5Crightarrow+%5Cmathbb%7BR%7D%5En)
,
![\rho_{data}: \Omega \rightarrow \mathbb{R}^n](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Ctextstyle+%5Crho_%7Bdata%7D%3A+%5COmega+%5Crightarrow+%5Cmathbb%7BR%7D%5En)
と,
ある分布ρとデータの分布ρ_dataに対して、<br>
![min_G max_D \{  \mathbf{E}_{x \sim \rho_{data}(\mathbf{x})} [\log{D(x)}] +  \mathbf{E}_{z \sim \rho(\mathbf{z})}[\log{(1 - D(G(z)))}] \}](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Cdisplaystyle+min_G+max_D+%5C%7B++%5Cmathbf%7BE%7D_%7Bx+%5Csim+%5Crho_%7Bdata%7D%28%5Cmathbf%7Bx%7D%29%7D+%5B%5Clog%7BD%28x%29%7D%5D+%2B++%5Cmathbf%7BE%7D_%7Bz+%5Csim+%5Crho%28%5Cmathbf%7Bz%7D%29%7D%5B%5Clog%7B%281+-+D%28G%28z%29%29%29%7D%5D+%5C%7D)
