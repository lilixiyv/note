# 教材知识
## 一、参数估计

### 1.0 统计量
**统计量** ：简单样本的函数，不含未知参数
**顺序统计量**：$X_{(n)}$ ，一组统计量中第n小的
#### 期望与方差
- $E(aX+bY+c) = aE(X)+bE(Y)+c$$
- X与Y相互独立$\rightarrow$ $E(XY)=E(X)E(Y)$
- $Var(X) = E[{X-E(X)}^2]=E(X^2)-{[E(X)]}^2$
- $Var(aX+b) = a^2 Var(X)$
- X与Y相互独立$\rightarrow$ $Var(X\pm Y)=Var(X) + Var(Y)$
#### 充分统计量
- 定义：$\{P_\theta , \theta \in \Theta\}$ ，当统计量$T(X)=t$时，X的条件分布与$\theta$无关，则$T(X)$为充分统计量
- 因式分解定理：
		$\{P_\theta , \theta \in \Theta\}$ 中，$T(X)$是充分的
		$\Leftrightarrow$ 
		$\exists$ 定义在$I \times \theta$上的函数$g(t,\theta)$及定义在$R^n$上的函数$h(x)$，s.t.
		$$
			p(x,\theta)=g(T(x),\theta)h(x)
	$$
#### 示性函数
$$
I_A (u)=
\begin{cases}
1,u \in A\\
0,u \notin A\\
\end{cases}
$$
### 1.1 频率估计
#### 参数估计
用统计量估计参数
#### 频率估计
用样本频率替换未知概率
### 1.2 矩估计
### 1.3 极大似然估计（MLE）
似然函数
$$L(\theta; x_1, x_2, \ldots, x_n)=\prod_{i=1}^n p(x_i;\theta)$$
一般求$$\frac{\partial ln L(\theta,x)}{\partial \theta_i} = 0$$
### 1.4 估计优良性
#### 均方误差 MSE
$$
MSE_\theta (T) =R(\theta, T) = E\{{[T(x)-q(\theta)]}^2\}
$$
若$R(\theta, T)<+\infty$ ，则
$$
R(\theta,T)=Var_\theta(T(x)) + b^2(\theta, T)
$$
其中$b(\theta,T)=E_\theta (T(x)-q(\theta))$
称为**偏差**

#### 非容许
两个估计量$T(X)$和$S(X)$，若满足
$$
R(\theta,T)\leq R(\theta,S)
$$
且对于某些$\theta$严格不等式成立，则$S$是非容许的
#### 无偏估计量
对$\forall \theta \in \Theta$ 有
$$
E(T(x)) = q(\theta)
$$
### 1.5 一致最小方差无偏估计 UMVUE
**存在性**
**唯一性**：概率1下UMVUE唯一
#### 完全性
$g(t)$为实值函数，若对$\forall \theta \in \Theta$，$E_\theta (g(T)) = 0$成立时必有$g(T)\equiv 0$，则$T(X)$是完全的
**定理**
$$
p(x,\theta) = c(\theta)h(x)\exp\left\{\sum_{k=1}^m w_k T_k(x) \right\}
$$
其中$w=w(\theta)\in \Omega \subset R^m$ 
若$\Omega$有内点，则$(T_1(x),\ldots,T_m(x))$是**完全充分**的
**定理** Lehmann-Scheffe
$S(x)$为完全充分统计量，$\varphi (x)$为$q(\theta)$的无偏估计
$\rightarrow$
$T(x)=E_\theta (\varphi(x)|S(x))$是$q(\theta)$的UMVUE
进一步，若$\forall \theta \in \Theta$，$Var_\theta(T(x)) < \infty$，则$T(x)$是$q(\theta)$唯一的UMVUE
### 1.6 信息不等式
#### Cramer-Rao族
(1)支撑$A=\{x:p(x,\theta)>0\}$与$\theta$无关，且对$\forall x \in A$，偏导$\frac{\partial}{\partial \theta} ln p(x,\theta)$存在
(2)$\forall \theta \in \Theta$，$T(x)$是满足$E_\theta |T| < \infty$ 任意统计量，则对$T(x)p(x,\theta)$，积分和微分可交换次序。
#### Fisher信息量

当仅有（1）成立时，定义：
$$
I(\theta)=E{[\frac{\partial}{\partial \theta} ln p(x,\theta)]}^2 (0\leq I(\theta) \leq \infty)
$$

当
$$
\frac{d^2}{d \theta ^2} \int_{-\infty}^{+\infty} p(x;\theta) dx = \int_{-\infty}^{+\infty} \frac{\partial^2 p(x;\theta)}{\partial \theta^2} dx
$$
成立时，有
$$
I(\theta) = - E_\theta [\frac{\partial^2}{\partial \theta^2} \ln p(x;\theta)]
$$
#### Cramer-Rao下界
$\frac{1}{I(\theta)}$
有：$\forall T(X) \in U_\theta$
$$ 
Var_\theta (T(X)) \geq \frac{1}{I(\theta)}
$$
其中$\forall \theta \in \Theta$，满足$Var_\theta (T(X)) < +\infty$，分布族为Cramer-Rao正则族，且$0<I(\theta)<+\infty$

#### 有效估计
无偏估计，方差达到信息不等式的下界，则为有效估计
#### 有效率
$$
e(\hat{q}(X)) = \frac{{(q'(\theta))}^2}{I(\theta)} / Var(\hat{q}(X))
$$
只有在指数分布族
$$
\left\{p(x;\theta)=c(\theta)\exp\left\{\sum_{k=1}^m w_k(\theta)T_k(\theta)\right\}h(x), \theta \in \Theta\right\}
$$
下，可估参数的有效估计才可能存在
#### 渐进无偏估计
$q(\theta)$的估计序列$\{T_n(X)\}$，$\forall \theta \in \Theta$，有$\lim_{n\rightarrow \infty} E_\theta(T_n(X)) = q(\theta)$
#### 渐进有效估计
$$
\lim_{n \rightarrow \infty} e(\hat{q}(X)) = 1
$$
### 1.7 相合估计
$\forall \varepsilon > 0$，有：
$$
\lim_{n \rightarrow \infty} P\{|\hat{q}_n (X) -q(\theta) > \varepsilon| \} = 0
$$
#### 定理
若$\hat{q}_n(X)$是$q(\theta)$的相合估计，且$h(y)$在$y=q(\theta)$处连续，则$h(\hat{q}_n)$是$h(q(\theta))$的相合估计

## 二、假设检验
### 2.1 势与势函数
#### 原假设和备择假设
统计模型：$\{P_\theta, \theta \in \Theta\}$
假设$H: \theta \in \bar{\Theta} \subset \Theta$$
原假设/零假设：所要检验的假设$H_0$
备择假设/对立假设：与$H_0$**不相容**的假设
假设检验问题：
$$
H_0: \theta \in \Theta_0, H_1: \theta \in \Theta_1
$$
简单假设：$\Theta_0$仅包含一个参数
复合假设
#### 拒绝域、接受域、检验统计量
检验：根据样本$x$，拒绝或接受$H_0$
样本空间分为不相交的子集拒绝域$W$和接受域$W^C$ 
检验统计量：当$H_0$时，可通过$T(x)$确定出拒绝域$W$
检验函数：拒绝域的示性函数
$$
\varphi(x) = 
\begin{cases}
1,x\in W\\
0,x \notin W
\end{cases}
$$
非随机化检验：$\varphi(x)=1$时，拒绝$H_0$，否则接受
Binomial试验：定义样本的函数$\varphi(x)$，值域为$[0,1]$，以$p=\varphi(x)$为成功概率
#### 两类错误
第一类错误：$H_0$为真时却拒绝之，概率为
$$
\alpha(\theta)=P_\theta\{x\in W\}, \theta \in \Theta_0
$$
第二类错误：$H_0$为假却接受之
#### 势
$H_0$不成立时拒绝$H_0$的概率：
$$
\gamma(\theta) = P_\theta\{x\in W\} = 1-\beta(\theta), \theta \in \Theta_1
$$
Neyman-Pearson检验原理：
在给定较小的数$\alpha (0<\alpha<1)$，在满足
$$
P_\theta\{x\in W\}\leq \alpha, \theta \in \Theta_0
$$
的方法中寻找使$\gamma(\theta)$尽可能大的检验方法。
其中$\alpha$为显著性水平
### 2.2 似然比检验
似然比：
$$
\lambda(x)=\frac{p(x_1,x_2,\ldots,x_n,\theta_1)}{p(x_1,x_2,\ldots,x_n,\theta_0)}
$$
似然比统计量：
$$
\lambda(x)= \frac{\sup_{\theta\in\Theta}\{p(x_1,\ldots,x_n,\theta\}}{\sup_{\theta\in\Theta_0}\{p(x_1,\ldots,x_n,\theta\}}
$$
检验的拒绝域为$W=\{x:\lambda(x)\leq c\}$ 
其中临界值$c$由$P\{\lambda(x)\leq c | H_0成立\}=\alpha$确定
#### 单边u-检验/z-检验
正态总体，方差已知
检验统计量
$$
U=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}
$$
拒绝域为：
$$
W=\{U:U\geq u_{1-\alpha}\}
$$
### 2.3 Neyman-Pearson引理
#### 最优势检验MPT
$\{P_\theta, \theta\in \Theta\}$，其中$\Theta=\{\theta_0,\theta_1\}$，考虑检验问题$H_0:\theta=\theta_0,H_1:\theta=\theta_1$
$\varphi^*(x)$是水平为$\alpha$检验，若对$\forall$水平为$\alpha$的检验$\varphi(x)$，有：
$$
E_{\theta_1}(\varphi^*(x)) \geq E_{\theta_1}(\varphi(x))
$$
则称$\varphi^*(x)$为水平为$\alpha$的最优势检验，简记为MPT
#### 引理
对给定的$\alpha \in (0,1)$，有：
- $\exists k\leq 0$及检验
	$$
	\varphi(x) = \begin{cases}
	1,if\ L(x)>k\\
	0,if\ L(x)<k
	\end{cases}
	\tag{2.3.1}
	$$
	其中$L(x)=\frac{p(x,\theta_1)}{p(x,\theta_0)}$，检验$\varphi(x)$是的MPT且满足
	$$E_{\theta_0}(\varphi(x))=\alpha \tag{2.3.2}$$
- 若$\varphi(x)$是水平为$\alpha$的MPT，则存在$k\geq 0$使得$\varphi(x)$满足$(2.3.1)$；若$\varphi(x)$满足$E_{\theta_0}(\varphi(x)) <1$，则$\varphi(x)$也满足$(2.3.2)$
### 2.4 最优势检验
### 2.5 一致最优势检验
#### 单边假设检验
对于检验问题
$$H_0:\theta \in \Theta_0,H_1:\theta\in \Theta_1$$
$\varphi^*(x)$是水平为$\alpha$检验，若对$\forall$水平为$\alpha$的检验$\varphi(x)$，有：
$$
E_{\theta_1}(\varphi^*(x)) \geq E_{\theta_1}(\varphi(x))
$$
则称$\varphi^*(x)$为水平为$\alpha$的一致最优势检验，简记为UMPT
#### 定理
若样本$x_1,\ldots,x_n$的联合密度$p(x,\theta)$是单参数的并可表示为：
$$
p(x,\theta)=d(\theta)h(x)\exp\left\{c(\theta)T(x)\right\}
$$
其中$c(\theta)$是关于$\theta$的严格单调递增函数，则对于单边检验问题：
$$
H_0:\theta\leq \theta_0,H_1:\theta>\theta_0
$$
1. 水平为$\alpha$的UMPT存在，其检验函数为
		$$
		\varphi^*(x)=
		\begin{cases}
		1,T(x)>c\\
		r,T(x)=c\\
		0,T(x)<c
		\end{cases}
		\tag{2.5.1}
		$$
		其中$c$和$r\in [0,1]$由$$E_{\theta_0}(\varphi^*(x))=\alpha$$确定
2. 水平为$\alpha$的UMPT的势函数$E_{\theta}(\varphi^*(x))$是关于$\theta$的增函数
3. 若$c(\theta)$为关于$\theta$的严格单调递减函数，则定理依然成立，只是需将$(2.5.1)$的不等号改变方向
4. 对假设检验问题$H_0:\theta=\theta_0;H_1:\theta>\theta_0$，结论依然成立 
#### 双边假设检验
对于假设问题
$$
H_0:\theta\leq\theta_1 or\  \theta\geq\theta_2;H_1:\theta_1<\theta<\theta_2
$$
若样本$x_1,\ldots,x_n$的联合密度$p(x,\theta)$是单参数的并可表示为：
$$
p(x,\theta)=d(\theta)h(x)\exp\left\{c(\theta)T(x)\right\}
$$
其中$c(\theta)$是关于$\theta$的严格单调递增函数，存在水平为$\alpha(0<\alpha<1)$的UMPT，其检验函数为：
$$
\varphi^*(x)=
\begin{cases}
1,c_1<T(x)<c_2\\
r_i,T(x)=c_i,i=1,2\\
0,T(x)<c_1\ or\ T(x)>c_2
\end{cases}
$$
其中四个常数$r_i,c_i(i=1,2)$由下式确定：
$$
E_{\theta_1}(\varphi^*(x))=E_{\theta_2}(\varphi^*(x))=\alpha
$$
### 2.6 无偏检验
对于假设问题：
$$
H_0:\theta=\theta_0;H_1:\theta\neq\theta_0
$$以及
$$
H_0:\theta_1\leq\theta\leq\theta_2;H_1:\theta<\theta_1\ or \ \theta>\theta_2
$$
其UMPT不存在
#### 无偏性
对于假设检验问题
$$H_0:\theta \in \Theta_0,H_1:\theta\in \Theta_1$$
设其检验函数$\varphi(x)$，若其势函数$g(\theta)=E_\theta(\varphi(x))$满足：
$$
\begin{cases}
g(\theta)\leq \alpha,\forall \theta \in \Theta_0\\
g(\theta)\geq \alpha,\forall \theta \in \Theta_1
\end{cases}
$$
则称$\varphi(x)$为水平为$\alpha$的**无偏检验**
UMPT一定是无偏检验
#### 一致最优势无偏检验UMPUT
若存在$\varphi^*(x)$是水平为$\alpha$的无偏检验，对$\forall$水平为$\alpha$的无偏检验$\varphi(x)$，有：
$$
E_{\theta_1}(\varphi^*(x)) \geq E_{\theta_1}(\varphi(x))
$$
则称$\varphi^*(x)$为水平为$\alpha$的一致最优势无偏检验，简记为UMPUT

#### 定理
对于假设问题
$$
H_0:\theta_1\leq\theta\leq\theta_2;H_1:\theta<\theta_1 or\  \theta>\theta_2
$$
若样本$x_1,\ldots,x_n$的联合密度$p(x,\theta)$是单参数的并可表示为：
$$
p(x,\theta)=d(\theta)h(x)\exp\left\{c(\theta)T(x)\right\}
$$
其中$c(\theta)$是关于$\theta$的严格单调递增函数，存在水平为$\alpha(0<\alpha<1)$的UMPUT，其检验函数为：
$$
\varphi^*(x)=
\begin{cases}
0,c_1<T(x)<c_2\\
r_i,T(x)=c_i,i=1,2\\
1,T(x)<c_1\ or\ T(x)>c_2
\end{cases}
$$
其中四个常数$r_i,c_i(i=1,2)$由下式确定：
$$
E_{\theta_1}(\varphi^*(T(x)))=E_{\theta_2}(\varphi^*(T(x)))=\alpha
$$

#### 定理
对于假设检验问题
$$H_0:\theta =\theta_0,H_1:\theta\neq\theta_0$$
定理其他部分一致，只是常数由下式确定：
$$
E_{\theta_0}(\varphi^*(T(x)))=\alpha\\
$$
$$
E_{\theta_0}(T(x)\varphi^*(T(x))) = \alpha E_{\theta_0}(T(x))
$$
# 常用定理与性质

## 两点分布可加性
## 泊松分布
$$
P(X=k)=\frac{\lambda^k e^{-\lambda}}{k!}
$$
则：
$$
E[X]=\lambda,Var(X)=\lambda
$$
### 可加性
$X_1\sim \lambda_1,X_2\sim \lambda_2$，则$X_1+X_2\sim Poisson(\lambda_1+\lambda_2)$
## 正态分布
### 正态分布与卡方分布
$$
Z_1,\ldots,Z_k \sim N(0,1)
$$
且相互独立，令$X=\sum_{i=1}^k Z_i^2$
有：
$$
X \sim \chi^2
$$
标准正态分布分位点
$z_\alpha$，左侧累积概率为$\alpha$的点
### 中心极限定理
大量独立样本的平均值分布都会趋近于正态分布
## 卡方分布
PDF为
$$
f(x; k) = 
\begin{cases} 
\dfrac{1}{2^{k/2} \Gamma(k/2)} \, x^{k/2 - 1} e^{-x/2} & \text{当 } x > 0 \\
0 & \text{当 } x \leq 0 
\end{cases}
$$
### Z检验
总体服从正态分布且方差$\sigma^2$已知，或样本量大到中心极限定理成立，有
$$
Z=\frac{\bar{X}-\mu_0}{\sigma/\sqrt{n}} \sim N(0,1)
$$

其中：
$$
\Gamma(z) = \int_0^\infty t^{z-1} e^{-t} \, dt, \quad \text{Re}(z) > 0
$$
若自由度为$k$，则
$$E[X]=k$$
$$Var(X)=2k$$
### 加法性质
$$
X_1 \sim \chi^2(k_1), X_2 \sim \chi^2(k_2)
$$
且相互独立，则：
$$
X_1+X_2 \sim \chi^2(k_1+k_2)
$$
## F分布
若
$$
X_1\sim \chi^2(v_1),X_2\sim \chi^2(v_2)
$$
且两者独立，则
$$
F=\frac{X_1/v_1}{X_2/v_2} \sim F(v_1,v_2)
$$
两组样本来自正态分布，样本方差分别为$S_1$、$S_2$，总体方差为$\sigma^2_1$ 、$\sigma_2^2$ ，则定义统计量：
$$
F=\frac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2}
$$
当$\sigma_1^2=\sigma_2^2$时，$F\sim F(v_1,v_2)$，其中$v_1=n_1-1,v_2=n_2-1$，为两组样本的自由度
## T分布
若
$$
Z\sim N(0,1),U\sim \chi^2(v)
$$
且两者独立，则定义：
$$
T=\frac{Z}{\sqrt{U/v}}
$$
则$T\sim t(v)$，其中$v=n-1$为自由度。                         
## 切比雪夫不等式

随机变量$X$，具有有限均值$\mu$和有限方差$\sigma^2$，则对$\forall \varepsilon>0$有：
$$
P(|X-\mu|\geq \varepsilon) \leq \frac{\sigma^2}{\varepsilon^2}
$$
## 马尔可夫不等式
**非负**随机变量$X$，且存在有限期望$E(x)$，则对$\forall a>0$，有：
$$
P(X\geq a) \leq \frac{E(X)}{a}
$$
