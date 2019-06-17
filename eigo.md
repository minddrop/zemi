# Bagging Predictor

## 4. Why Bagging Works

**_4.1 Numeric Prediction_**

Let each $(y,\boldsymbol{x})$ case in $\mathcal{L}$ be independently drawn from the probability distribution $P$. Suppose $y$ is numerical and $\phi (\boldsymbol{x},\mathcal{L})$ the predictor. Then the aggregated predictor is the average over $\phi (\boldsymbol{x},\mathcal{L})$, i.e.

$$ \phi_{ A }(\boldsymbol{x}) = E_{\mathcal{L}}(\phi(\boldsymbol{x},\mathcal{L})). $$

Take $\boldsymbol{x}$ to be a fixed input value and $y$ an output value. Then

$$ E_{\mathcal{L}}(y-\phi(\boldsymbol{x},\mathcal{L}))^2 = y^2-2yE_{\mathcal{L}}(\phi(\boldsymbol{x},\mathcal{L})) + E_{\mathcal{L}}(\phi^2 (\boldsymbol{x},\mathcal{L})). \tag{4.1} $$

Using $E_\mathcal{L}\phi(\boldsymbol{x},\mathcal{L})=\phi_A(\boldsymbol{x})$ and applying the inequality $EZ^2\geq (EZ)^2$ to the third term in $(4.1)$ gives

$$ E_{\mathcal{L}}(y-\phi(\boldsymbol{x},\mathcal{L}))^2 \geq (y-\phi_{A}(\boldsymbol{x}))^2 \tag{4.2} $$

Integrating both sides of $(4.2)$ over the joint $y$, $\boldsymbol{x}$ output-input distribution, we get that the mean-squared error of $\phi_{A}(\boldsymbol{x})$ is lower than the mean-squared error averaged over $\mathcal{L}$ of $\varphi(\boldsymbol{x},\mathcal{L})$.
&emsp;How much lower depends on how unequal the two sides of

$$ [E_{\mathcal{L}}(\varphi(\boldsymbol{x},\mathcal{L}))]^2 \leq E_{\mathcal{L}}(\varphi^2(\boldsymbol{x},\mathcal{L})) $$

are. The effect of instability is clear. If $\varphi(\boldsymbol{x},\mathcal{L})$ does not change too much with replicate $\mathcal{L}$ the two sides will be nearly equal, and aggregation will not help. The more highly variable the $\varphi(\boldsymbol{x},\mathcal{L})$ are, the more improvement aggregation may produce. But $\varphi_A$ always improves on $\varphi$.
&emsp;Now $\phi_A$ depends not only on $\boldsymbol{x}$ but also the underlying probability distribution $P$ from which $\mathcal{L}$ is drawn, i.e. $\phi_A = \phi(\boldsymbol{x},P)$. But the bagged estimate is not $\phi_A(\boldsymbol{x},P)$, but rather

$$\varphi_B(\boldsymbol{x}) = \varphi_A(\boldsymbol{x},P_\mathcal{L}),$$

where $P_\mathcal{L}$ is the distribution that concentrates mass $1/N$ at each point $(y_n,\boldsymbol{x}_n)\in{\mathcal{L}}$, ($P_\mathcal{L}$ is called the bootstrap approximation to P). Then $\varphi_B$ is caught in two currents: on the one hand, if the procedure is unstable, it can give improvement through aggregation. On the other side, if the procedure is stable, then $\varphi_B = \varphi_A(\boldsymbol{x},P_\mathcal{L})$ will not be as accurate for data drawn from $P$ as $\varphi_A(\boldsymbol{x},P)\simeq\varphi(\boldsymbol{x},\mathcal{L})$.
&emsp;There is a cross-over point between instability and stability at which $\varphi_B$ stops improving on $\varphi(\boldsymbol{x},\mathcal{L})$ and does worse. This has a vivid illustration in the linear regression subset selection example in the next section. There is another obvious limitation of bagging. For some data sets, it may happen that $\varphi(\boldsymbol{x}, \mathcal{L})$ is close to the limits of accuracy attainable on that data. Then no amount of bagging will do much improving. This is also illustrated in the next section.
