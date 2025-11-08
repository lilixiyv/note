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

# 常用定理与性质

## 两点分布可加性
