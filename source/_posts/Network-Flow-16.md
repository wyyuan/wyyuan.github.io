---
title: Network Flow Theroy -16
date: 2019-5-20 17:15:11
tags: 
- Network Flow Theroy
categories:
- 笔记
mathjax: true
---

&emsp;&emsp;这一篇笔记中涉及了原书的第16章内容

<!-- more -->

# VRP问题的思考

## Introduction
考虑一个最短路问题，它具有如下形式
$$
min \sum_{(i, j) \in A} c_{i j} x_{i j}\\
s.t.\sum_{\{j :(i, j) \in A \}} x_{i j}-\sum_{\{j :(j, i) \in A\}} x_{j i}=\left\{\begin{aligned} 1 & \text { for } i=1 \\ 0 & \text { for } i \in N-\{1, n\} \\-1 & \text { for } i=n \end{aligned}\right. \\
\sum_{(i, j) \in A} t_{i j} x_{i j} \leq T\\
x_{i j}=0 \text { or } 1 \quad \text { for all }(i, j) \in A
$$

## LAGRANGIAN RELAXATION TECHNIQUE

Origin problem (P)
$$
\begin{array}{c}{z^{*}=\min c x} \\ 
s.t. {\mathscr{A} x=b} \\
{x \in X}\end{array}
$$
构造拉格朗日松弛/子问题(Lagrangian relaxation / Lagrangian subproblem)
$$
\begin{array}{l}{\text { Minimize } c x+\mu(\Delta x-b)} \\ 
s.t.{x \in X}\end{array}
$$
**拉格朗日函数**(Lagrangian Function)定义为：
$$
L(\mu)=\min \{c x+\mu(\mathscr{A} x-b) : x \in X\}
$$
**Lemma (Lagrangian Bounding Priciple)** For any vector $\mu$ of the Lagrangian multipliers, the value L($\mu$) of the Lagrangian function is a lower bound on the optimal objective function value $z^*$ of the original optimization problem (P). 

这个定理表达为：
$$
z^{*} \geq \min \{c x+\mu(\mathscr{A} x-b) : x \in X\}=L(\mu)
$$
**拉格朗日乘子问题**(Lagrangian multiplier problem)
$$
L^{*}=\max _{\mu} L(\mu)
$$

**弱对偶性**(Weak Duality) The optimal objective function value $L^*$ of the Lagrangian multiplier problem is always a lower bound on the optimal objectivef unction value of the problem (P) .(i.e., $L^* \le z^*$). 

上述几个量之间的关系：
$$
L(\mu) \leq L^{*} \leq z^{*} \leq c x
$$
不等式约束的情况，拉格朗日乘子问题变为：
$$
L^{*}=\max _{\mu \geq 0} L(\mu)
$$
### Solving the Lagrangian Multiplier Problem 

​        根据上述定义，我们可以通过求解拉格朗日乘子问题来解决原问题。
$$
Max \ w \\
s.t. w \leq c x^{k}+\mu\left(\mathscr{A} x^{k}-b\right) \quad \text { for all } k=1,2, \ldots, K
$$

* 其中，$X=\{x^{1}, x^{2}, ...,x^K\}$是有限的。

这是一个线性规划问题，其中$\mu$是无约束的。接下来两章的内容是如何设计算法求得$\mu$。

### 一个例子

这里以一开始的最短路问题为例。
$$
L(\mu)=\min \left\{c_{P}+\mu\left(t_{P}-T\right) : P \in \mathscr{P}\right\}
$$
这里做了一些简化，因为我们不需要把路径守恒约束放到拉格朗日函数中，这样，原问题解的形式可以用路径来表达，这里一条路径$p$表示一系列$x$的取值。通过枚举所有路径 $p$ 可以得到所有 $c_{P}+\mu\left(t_{P}-T\right)$ 的取值。

![1558340610162](Network-FLow-16/1558340610162.png)

这样可以作出$L(\mu)$的图像：

![1558341703881](Network-FLow-16/1558341703881.png)

## 次梯度法 Bubgradient Optimization Technique 

>梯度法（爬山法）
>$$
>  \lim _{\theta \rightarrow 0} \frac{f(x+\theta d)-f(x)}{\theta}=\nabla f(x) d
>$$
>选取方向$d$使得$\nabla f(x) d>0$，则$d$就是“上山”方向。
>

次梯度法核心思想：不断按照一个迭代规则移动$\mu$
$$
\mu^{k+1}=\mu^{k}+\theta_{k}\left(\Delta x^{k}-b\right)
$$

* $x^k$是第$k$次迭代中任意一个解。

在使用这个方法的时候，步长$\theta_{k}$的选择较为重要。如果步长太小，算法会卡在一个地方不无法收敛；如果太大，则会漏掉最优解并且可能在两个或多个非优解之间来回。所以通过设置$\theta_{k} \rightarrow 0 $ 和 $ \sum_{j=1}^{k} \theta_{j} \rightarrow \infty$ 使得算法在这两种极端情况中取一个平衡点。

### 牛顿法(Newton's method)

### 不等式情况

$$
\mu^{k+1}=\left[\mu^{k}+\theta_{k}\left(\mathscr{A} x^{k}-b\right)\right]^{+}
$$

## LAGRANGIAN RELAXATION AND LINEAR PROGRAMMING 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxNjMyNTg5OCwtOTgxNjUzMTkyXX0=
-->