# Bagging Predictor
  
  
- Author
  LEO BREIMAN
  Statictics Department, University of California, Berkeley, CA 94720
  
- Presenter
  大前亮一
  OS4 年 1416020
  2019/04/25
  
## 4. どうしてバギングがうまくいくのか
  
  
### 4.1 数値予測
  
  
それぞれの<img src="https://latex.codecogs.com/gif.latex?&#x5C;mathcal{L}"/>の <img src="https://latex.codecogs.com/gif.latex?(y,&#x5C;boldsymbol{x})"/> は確率変数 P に従って独立に生じるとする. アンサンブル学習した回機器は<img src="https://latex.codecogs.com/gif.latex?&#x5C;phi%20(&#x5C;boldsymbol{x},&#x5C;mathcal{L})"/>を平均したものである. つまり,
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_{%20A%20}(&#x5C;boldsymbol{x})%20=%20E_{&#x5C;mathcal{L}}(&#x5C;phi(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))."/></p>  
  
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;boldsymbol{x}"/>を固定してとり、<img src="https://latex.codecogs.com/gif.latex?y"/>を真の数値として与える. すると,
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?E_{&#x5C;mathcal{L}}(y-&#x5C;phi(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))%20=%20y^2-2yE_{&#x5C;mathcal{L}}(&#x5C;phi(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))%20+%20E_{&#x5C;mathcal{L}}(&#x5C;phi^2(&#x5C;boldsymbol{x}),&#x5C;mathcal{L}).%20&#x5C;tag{4.1}"/></p>  
  
  
となり, 不等式 <img src="https://latex.codecogs.com/gif.latex?EZ^2&#x5C;geq%20(EZ)^2"/> を用いれば次のようになる.
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?E_{&#x5C;mathcal{L}}(y-&#x5C;phi(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))%20&#x5C;geq%20(y-&#x5C;phi_{A}(&#x5C;boldsymbol{x}))^2%20&#x5C;tag{4.2}"/></p>  
  
  
両辺級数をとると, アンサンブルした回機器 <img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_{A}(&#x5C;boldsymbol{x})"/> の MSE の方が, L から作った回機器より標準誤差が小さい.　どれだけ小さいかは下の不等式の両辺の値がどれだけ離れているかによる.
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?[E_{&#x5C;mathcal{L}}(&#x5C;varphi(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))]^2%20&#x5C;leq%20E_{&#x5C;mathcal{L}}(&#x5C;varphi^2(&#x5C;boldsymbol{x},&#x5C;mathcal{L}))"/></p>  
  
  
この不安定さの影響はわかりやすい. <img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi(&#x5C;boldsymbol{x},&#x5C;mathcal{L})"/> が <img src="https://latex.codecogs.com/gif.latex?&#x5C;mathcal{L}"/> ブートストラッピングで生成されたものとあまり変わらないのであれば、両辺はほとんど等しくなり, アンサンブル学習は標準誤差の減少に活かされないだろう. <img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi(&#x5C;boldsymbol{x},&#x5C;mathcal{L})"/> の変動が大きければ大きいほど, 回帰器はアンサンブル学習によってより改良される. しかし <img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi"/> は常に <img src="https://latex.codecogs.com/gif.latex?&#x5C;phi"/> の上位互換というわけではない.
　さて, <img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_A"/>は, <img src="https://latex.codecogs.com/gif.latex?&#x5C;boldsymbol{x}"/>だけでなく, そこから <img src="https://latex.codecogs.com/gif.latex?&#x5C;mathcal{L}"/> からサンプリングされた確率分布Ｐにも依存する. すなわち, <img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_A%20=%20&#x5C;phi(&#x5C;boldsymbol{x},P)"/>である. しかし, バギングの中身は <img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_A(&#x5C;boldsymbol{x},P)"/> ではなく,
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;phi_B(&#x5C;boldsymbol{x})%20=%20&#x5C;phi_A(&#x5C;boldsymbol{x},P_&#x5C;mathcal{L})"/></p>  
  
  
である. ここで, <img src="https://latex.codecogs.com/gif.latex?P_&#x5C;mathcal{L}"/> は各点 <img src="https://latex.codecogs.com/gif.latex?(y_n,&#x5C;boldsymbol{x}_n)&#x5C;in{&#x5C;mathcal{L}}"/>に <img src="https://latex.codecogs.com/gif.latex?1&#x2F;N"/> ずつ集中している分布である. (<img src="https://latex.codecogs.com/gif.latex?P_&#x5C;mathcal{L}"/> は, P まわりのブートストラップという.)
  
それから<img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi_B"/> は 2 つのパターンがあります. 1 つは, 不安定のときにアンサンブル学習によって改善する場合, もう片方は, 安定しているときで<img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi_B(&#x5C;boldsymbol{x})%20=%20&#x5C;varphi_A(&#x5C;boldsymbol{x},P_&#x5C;mathcal{L})"/>は<img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi_A(&#x5C;boldsymbol{x},P)&#x5C;simeq&#x5C;varphi(&#x5C;boldsymbol{x},P_&#x5C;mathcal{L})"/>のように分布 P に従うデータに対しては正確ではない.
  
安定性には, <img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi_B"/> の改良が止まり, <img src="https://latex.codecogs.com/gif.latex?&#x5C;varphi(&#x5C;boldsymbol{x},&#x5C;mathcal{L})"/> の改悪に変わる点があります. このことについては, 次の線形回帰サブセット選択のセクションにわかりやっすい説明があります. バギングにはこの他にも自明な制限があります. データセットによっては、<img src="https://latex.codecogs.com/gif.latex?&#x5C;phi(&#x5C;boldsymbol{x},%20&#x5C;mathcal{L})"/> がそのデータセットで実現できる精度の限界に近いことがある. バギングを限界まで行っても改善するわけではない. これについては次のセクションでも説明します.
  