# バギング

- Author
  LEO BREIMAN
  Statictics Department, University of California, Berkeley, CA 94720

- Presenter
  大前亮一
  OS4 年 1416020
  2019/04/25

## 4. どうしてバギングがうまくいくのか

### 4.1 数値予測

それぞれの$\mathcal{L}$の $(y,\boldsymbol{x})$ は確率分布 $P$ に従って独立に生じるとする. アンサンブル学習した回帰器は$\phi (\boldsymbol{x},\mathcal{L})$を平均したものである. つまり,

$$ \phi_{ A }(\boldsymbol{x}) = E_{\mathcal{L}}(\phi(\boldsymbol{x},\mathcal{L})). $$

$\boldsymbol{x}$を固定してとり、$y$ を真の数値として与える. すると,

$$ E_{\mathcal{L}}(y-\phi(\boldsymbol{x},\mathcal{L}))^2 = y^2-2yE_{\mathcal{L}}(\phi(\boldsymbol{x},\mathcal{L})) + E_{\mathcal{L}}(\phi^2 (\boldsymbol{x},\mathcal{L})). \tag{4.1} $$

となり, $E_\mathcal{L}\phi(\boldsymbol{x},\mathcal{L})=\phi_A(\boldsymbol{x})$ と $(4.1)$ 右辺第 3 項に不等式 $EZ^2\geq (EZ)^2$ を用いれば次のようになる.

$$ E_{\mathcal{L}}(y-\phi(\boldsymbol{x},\mathcal{L}))^2 \geq (y-\phi_{A}(\boldsymbol{x}))^2 \tag{4.2} $$

両辺級数をとると, アンサンブル学習した回帰器 $\phi_{A}(\boldsymbol{x})$ の MSE の方が, $\mathcal{L}$ から作った回帰器より標準誤差が小さい.　どれだけ小さいかは下の不等式の両辺の値がどれだけ離れているかによる.

$$ [E_{\mathcal{L}}(\varphi(\boldsymbol{x},\mathcal{L}))]^2 \leq E_{\mathcal{L}}(\varphi^2(\boldsymbol{x},\mathcal{L})) $$

この不安定さの影響はわかりやすい. $\varphi(\boldsymbol{x},\mathcal{L})$ が $\mathcal{L}$ ブートストラッピングで生成されたものとあまり変わらないのであれば、両辺はほとんど等しくなり, アンサンブル学習は標準誤差の減少に活かされないだろう. $\varphi(\boldsymbol{x},\mathcal{L})$ の変動が大きければ大きいほど, 回帰器はアンサンブル学習によってより改良される. しかし $\varphi_A$ は常に $\varphi$ の上位互換というわけではない.
　さて, $\phi_A$は, $\boldsymbol{x}$だけでなく, そこから $\mathcal{L}$ からサンプリングされた確率分布Ｐにも依存する. すなわち, $\phi_A = \phi(\boldsymbol{x},P)$である. しかし, バギングの中身は $\varphi_A(\boldsymbol{x},P)$ ではなく,

$$\varphi_B(\boldsymbol{x}) = \varphi_A(\boldsymbol{x},P_\mathcal{L})$$

である. ここで, $P_\mathcal{L}$ は各点 $(y_n,\boldsymbol{x}_n)\in{\mathcal{L}}$を $1/N$ でとる確率分布である, ($P_\mathcal{L}$ は, P まわりのブートストラップという). それから$\varphi_B$ は 2 つのパターンがあります. 1 つは, 不安定のときにアンサンブル学習によって改善する場合, もう片方は, 安定しているときで $\varphi_B(\boldsymbol{x}) = \varphi_A(\boldsymbol{x},P_\mathcal{L})$は$\varphi_A(\boldsymbol{x},P)\simeq\varphi(\boldsymbol{x},\mathcal{L})$のように分布 $P$ に従うデータに対しては正確ではない.
　安定性には, $\varphi_B$ の改良が止まり, $\varphi(\boldsymbol{x},\mathcal{L})$ の改悪に変わる点があります. このことについては, 次の線形回帰サブセット選択のセクションにわかりやっすい説明があります. バギングにはこの他にも自明な制限があります. データセットによっては、$\varphi(\boldsymbol{x}, \mathcal{L})$ がそのデータセットで実現できる精度の限界に近いことがある. バギングを限界まで行っても改善するわけではない. これについては次のセクションでも説明する.
